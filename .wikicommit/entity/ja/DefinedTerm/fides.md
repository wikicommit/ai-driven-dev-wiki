---
title: "FIDES"
type: "schema:DefinedTerm"
lang: ja
aliases: ["Flow Integrity Deterministic Enforcement System"]
tags: [エージェント, セキュリティ, エージェント安全性, エージェントアーキテクチャ]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/fides.md"
source_commit: "7b07912e0ef7183c203dba9eea44e8052dcec715"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Microsoft Agent Framework 向けにアーキテクチャ決定記録（ADR）の中で提案された、プロンプトインジェクションに対するラベルベースの情報フロー制御による防御策。コンテンツに完全性ラベルと機密性ラベルを付与し、それらをミドルウェアを通じて伝播させ、信頼できないコンテンツを変数参照の背後に置いてモデルのコンテキストの外に保持し、隔離された経路でのみ処理する。"
---

FIDES（ソースでは Flow Integrity Deterministic Enforcement System の略とされている）は、信頼できない外部コンテンツが AI エージェントの行動に影響を与えるのを防ぐことを目的とした、ラベルベースのセキュリティ設計である。これは Microsoft の `agent-framework` リポジトリにあるアーキテクチャ決定記録（ADR）で採用された選択肢であり、この ADR の日付は 2026 年 1 月 14 日、ステータスは *proposed*（提案中）である。ADR はこの設計を Costa et al.（2025）に帰しており、AI エージェントのための情報フロー制御に関するその研究を参考文献の一つに挙げている。

ADR が述べる問題は、[[DefinedTerm/prompt-injection]] に対する従来の防御がヒューリスティックとプロンプトエンジニアリングに依存しており、それらは決定論的ではなく回避され得るという点である。ADR が代わりに得ようとしているのは、信頼できないコンテンツがエージェントの振る舞いに影響を与えることを防ぎ、検証可能なセキュリティ保証を与え、コンプライアンスのための監査証跡を維持し、フレームワークの既存のミドルウェアパイプラインに非侵襲的に統合され、しかもオプトインかつ後方互換であり続ける、体系的な仕組みである。

## 用法

ADR は 4 つの中核コンポーネントを説明している。

- **コンテンツのラベル付け** — `IntegrityLabel`（TRUSTED / UNTRUSTED）と `ConfidentialityLabel`（PUBLIC / PRIVATE / USER_IDENTITY）を、最も制限の強いものが優先されるポリシーのもとで組み合わせる。
- **ミドルウェアによる強制** — ラベルを自動的に伝播させる `LabelTrackingFunctionMiddleware` と、呼び出しの実行前にポリシーを検査する `PolicyEnforcementFunctionMiddleware`。
- **変数による間接参照** — 信頼できないコンテンツを LLM のコンテキストから物理的に隔離しておく `ContentVariableStore` と `VariableReferenceContent`。
- **隔離された実行** — 信頼できないデータを監査ログ付きで隔離して処理する `quarantined_llm` ツールと `inspect_variable` ツール。

リモートの MCP 統合について、ADR は 2 つの仕組みを追加している。`readOnlyHint` や `openWorldHint` といった MCP の `ToolAnnotations` は FIDES のツールプロパティ（`source_integrity`、`accepts_untrusted`、`max_allowed_confidentiality`）に対応付けられ、サーバーの結果メタデータ `_meta.ifc` はアイテムごとの `security_label` 値へと解析されるため、提供元が付与したラベルがミドルウェアによって強制される。ADR の実装ノートによれば、`SecureMCPToolProxy` は MCP のツールや URL に接続する際にこれらのラベルを自動的に適用し、`X-MCP-Features: ifc_labels` を公開しているサーバーについては `_meta.ifc` のラベルが正とされ、明示的に `readOnlyHint=True` と指定されていないツールはすべて潜在的なシンクとして扱われ、情報の持ち出しを防ぐために既定で `max_allowed_confidentiality=PUBLIC` となる。ラベルのないコンテンツは既定で UNTRUSTED となる。

ADR は FIDES を、退けた 4 つの代替案と比較検討している。プロンプトエンジニアリングによる防御は非決定論的で回避可能だとし、コンテンツのサニタイズは計算コストが高く、偽陽性が多く、未知の攻撃に対処できないとしている。エージェントインスタンスの分離は強い隔離をもたらすことは認めつつも、オーバーヘッドが大きくインスタンス間の状態管理が難しいとし、ランタイム監視のみに頼る方式は事前的ではなく事後的であり、予防的な保証を提供できないとしている。

## 適用される場面

ADR は FIDES をオプトインかつ完全に後方互換なものとして提示している。セキュリティミドルウェアを持たないエージェントは通常どおり機能し、中核のコンテンツ型やエージェントのロジックは変わらず、ポリシーはエージェント単位またはツール単位で設定できる。ADR が挙げる前提条件は、フレームワークの既存の `FunctionMiddleware` 基底クラス、スキーマ変更を不要にするために `additional_properties` に載せて運ばれるラベル、そしてラベルを永続化するための `SerializationMixin` である。

ADR 自身が挙げる欠点も同様に明示的である。ミドルウェアはすべてのツール呼び出しにレイテンシを加え、変数ストアは信頼できないコンテンツのためにメモリを消費する。開発者はラベルの仕組みを理解し、信頼できない入力を受け付けるツールの明示的な許可リストも含めて、ツールのポリシーを手作業で設定しなければならない。最も制限の強いものが優先される伝播は、場合によっては過度に保守的になり得る。そしてこの設計はすべての攻撃ベクトルを防ぐわけではなく、その例として訓練データの汚染が挙げられている。パフォーマンスベンチマークとユーザー受け入れテストの 2 項目は、文書中で未チェックのまま残されている。

これがどの程度確立したものかは、文書自身のヘッダーが示している。これはステータスが *proposed*（提案中）のアーキテクチャ決定記録であり、したがってそこに記録されているのは、単一のフレームワークの中で提示された決定である。この設計がそのフレームワークの外で出荷されたのか、あるいは評価されたのかについて、記録はどちらとも述べていない。

## 関連用語

- [[DefinedTerm/prompt-injection]] — この設計が対象とする攻撃の種類
- [[DefinedTerm/indirect-prompt-injection]] — 取得されたコンテンツを通じて届く変種
- [[SoftwareApplication/microsoft-agent-framework]] — この ADR が属するフレームワーク
- [[DefinedTerm/model-context-protocol]]
