---
title: "FIDES"
type: "schema:DefinedTerm"
lang: ja
aliases: ["Flow Integrity Deterministic Enforcement System"]
tags: [エージェント, セキュリティ, エージェント安全性, エージェントアーキテクチャ]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/fides.md"
source_commit: "7b07912e0ef7183c203dba9eea44e8052dcec715"
translated_at: "2026-09-22"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "Microsoft Agent Framework 向けにアーキテクチャ決定記録で提案された、プロンプトインジェクションに対するラベルベースの情報フロー制御による防御。内容に完全性と機密性のラベルを付し、それをミドルウェアを通じて伝播させ、信頼できない内容を変数参照の背後に置いてモデルのコンテキストの外に保ち、隔離された経路でのみ処理する。"
---

FIDES——出典では Flow Integrity Deterministic Enforcement System の略とされる——は、信頼できない外部の内容が
AI エージェントの行動に影響することを防ぐことを意図した、ラベルベースのセキュリティ設計である。これは
Microsoft の `agent-framework` リポジトリにあるアーキテクチャ決定記録で選ばれた選択肢であり、日付は 2026 年
1 月 14 日、ステータスは*提案中*で、設計を Costa ら（2025）に帰し、AI エージェントの情報フロー制御に関する
その研究を参考文献に挙げている。

同 ADR が述べる問題は、[[DefinedTerm/prompt-injection]] に対する従来の防御がヒューリスティクスとプロンプト
エンジニアリングに依拠しており、決定論的でなく迂回されうるということである。代わりに得ようとしているのは、
信頼できない内容がエージェントの振る舞いに影響することを防ぎ、検証可能なセキュリティ上の保証を与え、
コンプライアンスのための監査証跡を維持し、フレームワーク既存のミドルウェアのパイプラインへ非侵襲的に統合され
つつ、オプトインかつ後方互換であり続ける、体系的な機構である。

## 用法

同 ADR は 4 つの中核的な構成要素を記述している。

- **内容へのラベル付け** — `IntegrityLabel`（TRUSTED / UNTRUSTED）と `ConfidentialityLabel`
  （PUBLIC / PRIVATE / USER_IDENTITY）を、最も制限的なものが勝つという方針のもとで組み合わせる。
- **ミドルウェアによる強制** — ラベルを自動的に伝播させる `LabelTrackingFunctionMiddleware` と、呼び出しが
  実行される前にポリシーを検査する `PolicyEnforcementFunctionMiddleware`。
- **変数による間接参照** — 信頼できない内容を LLM のコンテキストから物理的に隔離しておく
  `ContentVariableStore` と `VariableReferenceContent`。
- **隔離された実行** — 信頼できないデータを監査ログを伴って隔離のうちに処理する `quarantined_llm` と
  `inspect_variable` のツール。

リモートの MCP 統合について、同 ADR は 2 つの機構を加える。`readOnlyHint` や `openWorldHint` といった MCP の
`ToolAnnotations` が FIDES のツール属性（`source_integrity`、`accepts_untrusted`、
`max_allowed_confidentiality`）へ写され、サーバーの `_meta.ifc` という結果のメタデータが項目ごとの
`security_label` の値へ解析されて、提供側が付したラベルがミドルウェアによって強制されるようにする。その
実装上の注記は、`SecureMCPToolProxy` が MCP のツールないし URL への接続時にこれらのラベルを自動的に適用すること、
`X-MCP-Features: ifc_labels` を告知するサーバーについては `_meta.ifc` のラベルが正典となること、そして
`readOnlyHint=True` と明示的に印されていないツールはすべて、情報の持ち出しを防ぐために
`max_allowed_confidentiality=PUBLIC` を既定とする潜在的なシンクとして扱われることを述べている。ラベルの付いて
いない内容は既定で UNTRUSTED となる。

同 ADR は FIDES を、退けた 4 つの代替案と比較検討している。プロンプトエンジニアリングによる防御は非決定論的で
迂回可能だとする。内容のサニタイズは計算上高価で偽陽性が多く新手の攻撃を扱えないとする。エージェントの
インスタンスを分けることは強い隔離を与えると認めつつ、オーバーヘッドが高くインスタンス間の状態の扱いが
難しいとする。そして実行時の監視だけでは、能動的ではなく受動的であり、予防的な保証を与えられないとする。

## 適用条件

同 ADR は FIDES をオプトインかつ完全に後方互換なものとして提示している。セキュリティのミドルウェアを持たない
エージェントは通常どおり機能し、中核の内容型やエージェントのロジックは変更されず、ポリシーはエージェントごと
ないしツールごとに設定可能である。述べられている前提条件は、フレームワーク既存の `FunctionMiddleware` 基底
クラス、スキーマ変更が不要になるよう `additional_properties` に載せて運ばれるラベル、そしてラベルの永続化のための
`SerializationMixin` である。

その欠点の一覧も同様に明示的だ。ミドルウェアはあらゆるツール呼び出しに遅延を加え、変数ストアは信頼できない
内容のためにメモリを消費する。開発者はラベルの体系を理解し、信頼できない入力を受け付けるツールの明示的な
許可リストを含めて、ツールのポリシーを手で設定しなければならない。最も制限的なものが勝つという伝播は場合に
よっては過度に保守的でありうる。そしてこの設計はすべての攻撃経路を防ぐわけではなく、訓練データの汚染がその
例として挙げられている。2 つの項目——性能のベンチマークとユーザー受け入れテスト——は文書内で未チェックのまま
残されている。

どれほど確立しているかは、文書自身の冒頭が述べている。これはステータス*提案中*のアーキテクチャ決定記録であり、
記録しているのは単一のフレームワークの内部で提出された決定である。この設計が出荷されたか、あるいはその外で
評価されたかについては、この記録は何も述べていない。

## 関連用語

- [[DefinedTerm/prompt-injection]] — この設計が狙う攻撃の類
- [[DefinedTerm/indirect-prompt-injection]] — 取得された内容を経由して届く型
- [[SoftwareApplication/microsoft-agent-framework]] — この ADR が属するフレームワーク
- [[DefinedTerm/model-context-protocol]]
