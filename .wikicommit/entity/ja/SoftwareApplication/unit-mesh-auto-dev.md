---
title: "AutoDev (unit-mesh/auto-dev)"
type: "schema:SoftwareApplication"
lang: ja
tags: [コーディングツール, コードレビュー, マルチエージェント, コーディングエージェント, オープンソース]
translated_from: ".wikicommit/entity/en/SoftwareApplication/unit-mesh-auto-dev.md"
source_commit: "19bc48f9255734f269436c88f52086be2c4420a5"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "GitHub リポジトリ unit-mesh/auto-dev で公開されているオープンソースの AI コーディングツール。VS Code 版を含む IDE プラグイン、CLI、デスクトップアプリケーション、GitHub Actions 上で動作する Remote Agent を備える。エージェント型コードレビューは、差分、lint、issue、テスト、コード構造の情報をマルチエージェントアーキテクチャと組み合わせて、変更を分析し修正を生成する。"
  applicationCategory: "AI コーディングツール"
  softwareVersion: "1.8（IDE プラグイン、2024 年 4 月）、0.3.0（CLI、2025 年 11 月）、compose-0.3.0（Desktop、2025 年 11 月）"
  featureList: "要求に紐づいたコミットメッセージ生成、コードスメルに基づくリファクタリング、AI による名前変更の提案、ターミナルコマンド生成などの IDE プラグイン機能（1.8）、GitHub Actions 上または MCP サービスとして issue の分析、タスク計画、コーディングを行う AutoDev Remote Agent、エージェント型コードレビュー（autodev review）、Git の差分、CodeGraph、リンター、issue、テストからの静的情報収集、構造化されたレビュー指摘、修正計画の生成、CodingAgent による自動修正"
---

AutoDev は、GitHub リポジトリ `unit-mesh/auto-dev` でリリースが公開されている AI コーディングツールである。このページはそのリポジトリのツールを扱う。[[SoftwareApplication/autodev]] は、同じ名前を持つ別のフレームワークについての別ページである。[[BlogPosting/ai-code-review-evolved-autodev-multi-agent-architecture]] の説明によれば、npm パッケージ `@autodev/cli` から CLI としてインストールするか、AutoDev Desktop としてダウンロードすることができる。

作者の説明によれば、そのコードレビュー機能が取り組む問題は、レビュアーが必要とする情報（lint の結果、テスト、issue、変更履歴）が複数のシステムに散在していること、複雑なロジックを理解できる単一のツールが存在しないこと、そして手作業のレビューは遅く主観的であることである。

## 機能

### IDE プラグイン

作者は AutoDev をコード変更のアシスタントとして位置づけている。新しい要求のたびにコードを再生成するのではなく、デベロッパーが既存のコードを変更するのを支援するものであり、そのためには規約、ベストプラクティス、ソフトウェアのナレッジエンジニアリングをツールに組み込む必要があると彼は主張している。[[BlogPosting/evolutionary-ai-assisted-coding-with-devops-practices]] で説明されているプラグインのバージョン 1.8 は、その方向に沿った機能をいくつか追加した。社内の OA システムから取得したユーザーの現在の要求 ID とコード変更をもとに生成されるコミットメッセージ、IDE 自身のインスペクションが報告するコードスメルに基づくリファクタリング、ユーザーが IDE の名前変更機能を呼び出したときに提示される 5 つの AI による名前の候補（設定で手動で有効化する）、そして日付、オペレーティングシステム、シェルをコンテキストに含めるターミナルコマンド生成である。同じバージョンでは、中国語の設定ページとプロンプト、より簡単な LLM サーバーのテスト、2024.1 版 IDE のサポート、AutoSQL の改善も追加された。

### コードレビュー

CLI のバージョン 0.3.0 では、レビューは `autodev review -p .` で実行する。レビューは 4 ステップのパイプラインとして進む。まず静的情報を収集する（Git の差分から得られる変更ハンク、CodeGraph などのツールで特定した影響を受けるクラスとメソッド、ESLint、Ktlint、Detekt などのリンターの結果、関連する issue とテスト）。次に、選択したレビュー種別（総合、パフォーマンス、セキュリティ、スタイル）に沿って LLM にそれを分析させ、構造化された指摘を作成する。続いて lint と AI の指摘を統合して優先順位を付け、ユーザーが編集できる修正計画にまとめる。最後に、ロールバックや反復が可能なパッチとして修正を生成する。

作業は複数のエージェントに分担される。メインの CodeReviewAgent が情報を集約してオーケストレーションを行い、分析用のサブエージェント（AnalysisAgent、ErrorRecoveryAgent、CodebaseInvestigatorAgent）が大きなコンテンツ、エラーからの回復、リポジトリ全体の調査を担当し、CodingAgent が `read_file`、`write_file`、lint、テストなどのツール呼び出しを通じてコードを変更する。サブエージェントは `SubAgentManager` によって管理され、すべてのツールは `ToolRegistry` に登録されて `ToolOrchestrator` を通じて実行される。

### AutoDev Remote Agent

AutoDev Remote Agent は AutoDev Workbench の一部で、`unit-mesh/autodev-workbench` リポジトリで公開されており、[[BlogPosting/autodev-remote-coding-agent]] での発表のとおり、2025 年 6 月に試用段階に入った。サーバー上の MCP サービスとして、あるいは GitHub プロジェクトの Actions の中で実行でき、GitHub の issue を分析し、タスクを計画し、コードを書き、その分析と計画を issue に書き戻す。ツール設計は AutoDev Sketch のものを踏襲しており、MCP でラップした汎用ツールの上に GitHub 用のツールを追加している。また、ラウンド数の上限によって会話が際限なくループするのを防いでいる。サンドボックス化は、GitHub Action の中に完全なコード実行環境を作ることと、新しい GitHub Actions を動的に作成することに依拠している。

## 採用とエコシステム

作者は、個人が IDE を保守するコストを理由に、AutoDev は独自の IDE の構築には注力しないと述べている。また、リモートエージェントは、コーディングモデルがエージェント的にコーディングできるようになったことで、エージェントがサーバー上で動作してコードを書き、テストし、デプロイできるようになるという見方を反映したものだという。Remote Agent の最初のバージョンは、AutoDev の VS Code 版からリファクタリングで切り出したコアをもとに、Augment コーディングアシスタントの助けを借りて設計された。それ自身をブートストラップさせることが、表明されている次の目標である。

コードレビューについては、作者は今後のバージョンでテストカバレッジ、CI/CD、インクリメンタル分析を統合すると述べている。
