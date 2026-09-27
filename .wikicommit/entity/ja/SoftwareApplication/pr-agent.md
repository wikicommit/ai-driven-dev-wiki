---
title: "PR-Agent"
type: "schema:SoftwareApplication"
lang: ja
tags: [コードレビュー, コーディングツール, エージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/pr-agent.md"
source_commit: "abe7dbaa9cb573068b927bda52cc565d6ba058e6"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Qodo が開発し、その後オープンソースコミュニティに寄贈された、オープンソースのプルリクエストレビューエージェント。機能はスラッシュコマンドとして公開されており、プルリクエストのコメントまたは CLI から実行する。"
  applicationCategory: "コードレビュー"
  featureList: "/describe, /review, /improve, /ask, /similar_issue"
  author: "[[Organization/qodo]]"
---

PR-Agent は、プルリクエストを対象に動作する、オープンソースの AI 駆動コードレビューエージェントである。README は自らを「The Original Open-Source PR Reviewer」と称し、これを開発した企業である [[Organization/qodo]] の、コミュニティによって保守されるレガシープロジェクトだと説明している。MIT ライセンスで公開されており、独自のサイト <https://www.pr-agent.ai> とドキュメント <https://docs.pr-agent.ai> を持つ。

プロジェクトの機能はスラッシュコマンドとして公開されており、プルリクエスト上のコメントとして実行するか、CLI からプルリクエストの URL を指定して実行する。`/describe`、`/review`、`/improve`、`/ask` はプルリクエストに対して動作し、`/similar_issue` は代わりに Issue を対象とする。README によれば、`/review`、`/improve`、`/ask` はそれぞれ 1 回の LLM 呼び出しで実行され、所要時間はおよそ 30 秒、コストは低いとされている。

README は、このプロジェクトを Qodo 自身の現行製品と区別している。後者は機能が豊富でコンテキストを考慮した体験として説明される一方、PR-Agent 自体はコミュニティによって保守されるレガシープロジェクトと位置づけられている。README はまた、このリポジトリが Qodo によるオープンソースプロジェクト向けの無料枠ではないことを明言しており、それは Qodo が別途提供しているものである。

## 機能

上記のコマンド群がインターフェースである。README が説明を添えているのはそのうち 2 つだけで、`/ask` はプルリクエストについての自由形式の質問を受け付け、`/similar_issue` は指定した Issue に類似するリポジトリ内の Issue を見つける。それ以外のコマンドは名前が列挙されるのみで、機能と Git プロバイダーの対応表や各ツールの個別ページについてはドキュメントサイトに委ねている。一方で、`/help_docs` は認証情報の露出に関する問題の修正待ちのため `v0.36.1` 以降一時的に無効化されていると記しており、あるインストール環境で利用できるコマンドの集合は、実行しているバージョンによって異なる。

個々のコマンドではなくプロジェクト全体について主張されている特性が 2 つある。1 つは PR 圧縮戦略で、これにより小規模なプルリクエストも大規模なプルリクエストも効果的に処理できるとされている。もう 1 つは、プロンプトが JSON ベースであることで、README はこれを、ツール自体を編集することなく設定ファイルを通じてレビューのカテゴリや振る舞いをカスタマイズできる理由として挙げている。

README には、レビュー出力を特定のモデルに結びつける記述はない。使用可能なモデルとして挙げられているのは、OpenAI の GPT、Anthropic の Claude、Google の Gemini、DeepSeek、Mistral であり、それ以外にも [[SoftwareApplication/litellm]] 経由で到達できるあらゆるモデルが使える。README はこのリストを Azure OpenAI、AWS Bedrock、Vertex AI、Databricks、OpenRouter、Ollama にまで広げている。

## 採用とエコシステム

PR-Agent は、レビューを行う Git ホスティング基盤とデプロイ方法の両面で、プラットフォームに依存しない。対応する Git プロバイダーは GitHub、GitLab、BitBucket、Azure DevOps、Gitea であり、デプロイ形態は CLI、GitHub Action、Docker、セルフホスト型インスタンス、Webhook である。README が最初に示すクイックスタートの手順は、プロジェクト自身のアクションを参照する GitHub Actions ワークフローと、`pip install pr-agent` の後に API キーを環境変数に設定して CLI を呼び出す方法である。

Docker イメージは、プロジェクトの途中で名前空間が変わった。`0.34.2` 以降のリリースは `pragent/pr-agent` で公開されている一方、`v0.31` までのリリースは以前の `codiumai/pr-agent` 名前空間に、新しいイメージが追加されない凍結されたアーカイブとして残っている。README は、この境界をまたいでアップグレードする際には、固定しているイメージの参照を更新するよう求めている。

プロジェクトのガバナンスも移行している。Qodo はこのプロジェクトをオープンソースコミュニティに寄贈し、現在は独自の GitHub Organization に置かれている。リポジトリは `The-PR-Agent/pr-agent` として公開されており、クイックスタートの GitHub Actions ワークフローはアクションを `the-pr-agent/pr-agent@main` として参照している。プロジェクトは完全にコミュニティが所有するものと説明され、新たなメンテナーを受け入れており、初の外部メンテナーも加わった。README によれば、オープンソース財団への寄贈の手続きが進められており、ドキュメントは docs.pr-agent.ai に移行した。Qodo は引き続きゴールドスポンサーであり、プロジェクトの継続的な開発はスポンサーによって支えられていると記した見出しの下に掲載されている。
