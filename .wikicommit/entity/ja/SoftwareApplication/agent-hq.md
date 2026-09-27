---
title: "Agent HQ"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール, エージェントオーケストレーション, ガバナンス]
translated_from: ".wikicommit/entity/en/SoftwareApplication/agent-hq.md"
source_commit: "a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "サードパーティのコーディングエージェントを GitHub フローの中でネイティブに実行するための GitHub のプラットフォーム層。複数のサーフェスにまたがる司令塔、エディター側での計画とカスタマイズ、エンタープライズ向けのガバナンス制御を組み合わせている。"
  applicationCategory: "エージェントオーケストレーションプラットフォーム"
  featureList: "1 つの Copilot サブスクリプションで使えるサードパーティのコーディングエージェント、GitHub・VS Code・モバイル・CLI にまたがる mission control、ブランチ制御とエージェントアイデンティティ、VS Code の Plan Mode とカスタムエージェント、GitHub MCP Registry、エージェントコントロールプレーン、Copilot メトリクスダッシュボード"
  author: "[[Organization/github]]"
---

Agent HQ は、コーディングエージェントを GitHub フローに後付けするのではなく、GitHub フローにネイティブなものにする取り組みに GitHub が付けた名前である。GitHub Universe 2025 で発表されたもので（[[BlogPosting/introducing-agent-hq]] を参照）、GitHub はこれを、複数のベンダーのエージェントを 1 つのプラットフォームにまとめるオープンなエコシステムと説明しており、各ベンダー独自のサーフェスではなく、有料の [[SoftwareApplication/github-copilot]] サブスクリプションを通じて利用できる。GitHub は、発表後の数か月のうちに、Anthropic、OpenAI、Google、Cognition、xAI のエージェントがこの形で利用可能になると述べている。

Agent HQ が意図的に変えないものも、GitHub による定義の一部になっている。作業の基本要素は Git、プルリクエスト、Issue のままで、計算資源も GitHub Actions またはセルフホストランナーのままである。Agent HQ が加える層は指揮とガバナンス、すなわちエージェントの作業を割り当てて追跡するための 1 つの場所、エージェントの振る舞い方に対するエディター側の制御、そしてそもそもどのエージェントの実行を許可するかに対する管理者向けの制御である。

## 機能

- **Mission control** — GitHub が、単一の行き先ではなく、GitHub、VS Code、モバイル、CLI にまたがる一貫したインターフェースと説明する司令塔。開発者はここからエージェント群の中から選び、作業を並行して割り当て、どのデバイスからでも進捗を追跡できる。
- **ブランチ制御** — エージェントが作成したコードに対して CI やその他のチェックがいつ実行されるかを、きめ細かく監督できるようにする。
- **エージェントアイデンティティ** — どのエージェントがタスクを構築しているか、そのアクセス権、適用されるポリシーを、人間のチームメンバーと同じように管理できるようにする。
- **ワンクリックでのマージコンフリクト解決**、ファイルナビゲーションの改善、コードコメント機能の改善。
- **統合** — Slack と Linear との統合。以前に発表されていた Atlassian Jira、Microsoft Teams、Azure Boards、Raycast との連携に加わる。
- **VS Code の Plan Mode** — 実装の前に Copilot が明確化のための質問をして段階的な進め方を組み立てる。計画が承認されると、それが Copilot に渡され、ローカルで、またはクラウドエージェントを通じて実装される。
- **[[DefinedTerm/agents-md]] ファイルで設定するカスタムエージェント** — ソース管理される文書で、再度プロンプトを与えることなくエージェントの振る舞いを形づくるルールとガードレールを記述する。加えて、独自のシステムプロンプトとツールを持つ GitHub Copilot のカスタムエージェントもある。
- **VS Code の GitHub MCP Registry** — [[DefinedTerm/model-context-protocol]] サーバーをワンクリックで発見、インストール、有効化できる。GitHub は、MCP の仕様全体をサポートしているエディターは VS Code だけだと述べている。
- **エージェントコントロールプレーン** — エンタープライズの管理者向けのガバナンス層で、セキュリティポリシー、監査ログ、アクセス管理、どのエージェントを許可するか、そしてそれらがどのモデルにアクセスできるかを扱う。発表時点ではパブリックプレビュー。
- **Copilot メトリクスダッシュボード** — 発表時点ではパブリックプレビューで、組織全体での Copilot の利用状況と効果を報告する。

## 採用状況とエコシステム

GitHub は Agent HQ を、能力ではなくコード品質の観点から述べた問題への対策として位置づけている。レビューは通っても（「LGTM」）、その変更によってコードベースが劣化し、長期的な技術的負債になりうるという問題である。Agent HQ と同時にパブリックプレビューとして発表された GitHub Code Quality は、Copilot のセキュリティチェックを、変更されたコードが保守性と信頼性に与える影響にまで広げ、組織全体での可視化とレポート機能を加える。これとは別に、[[SoftwareApplication/github-copilot-coding-agent]] 自身のワークフローの中にコードレビューのステップが追加され、その出力が人間の目に触れる前に一次レビューを受けるようになった。

最初に登場したパートナーエージェントは [[SoftwareApplication/openai-codex]] で、GitHub は発表の週に VS Code Insiders の Copilot Pro+ ユーザー向けにこれを提供した。パートナーエージェントの中で、自身のネイティブなサーフェスを越えてエディターにまで広がった最初のものと説明されている。

以上はすべて、GitHub が発表しようとしていたプラットフォームについての GitHub 自身の説明であり、実際に提供された動作についての独立した報告ではない。また、いくつかの機能は執筆時点で今後提供予定、またはパブリックプレビューとされている。
