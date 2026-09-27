---
title: "Antigravity SDK"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングツール, エージェントアーキテクチャ, ローカルモデル, コードレビュー]
translated_from: ".wikicommit/entity/en/SoftwareApplication/antigravity-sdk.md"
source_commit: "9b65710f8033cfb0f6c3388db1436c4e823817a3"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Google Antigravity 製品ファミリーの Python SDK。ローカルモデルを相手にする場合も含め、Antigravity のエージェントをプログラムから構築・実行するためのもの。"
  applicationCategory: "エージェント開発 SDK"
  featureList: "エージェント設定オブジェクト、ライフサイクルフック、許可・拒否・ユーザーへの確認による安全ポリシー、MCP サーバーとの統合、サブエージェント、Web 検索・URL 取得・コマンド実行・スケジューリングなどの組み込みツール、LiteRT および OpenAI 互換エンドポイントを介したローカルモデル、予算とコンテキストのコンパクションの制御、OpenTelemetry によるトレーシング"
  author: "[[Organization/google]]"
---

Antigravity SDK は、[[SoftwareApplication/google-antigravity]] 製品ファミリーの Python 向けソフトウェア開発キットであり、`google.antigravity` パッケージとして公開されている。デスクトップアプリ、IDE、[[SoftwareApplication/antigravity-cli]] が開発者の前にエージェントを置くのに対し、SDK は開発者が自分の Python コードから Antigravity のエージェントを設定し実行できるようにする。製品のチェンジログには、0.1.1（2026 年 5 月 29 日）から 0.1.18（2026 年 9 月 21 日）までのリリースが掲載されている。

エージェントは、Python クライアントが接続するローカルのハーネスプロセスを通じて実行される。チェンジログはこれを `localharness` バイナリと呼んでいる。設定は `AgentConfig` や `LocalAgentConfig` といったオブジェクトとして表現され、リリース履歴の多くは、モデル、リトライ、予算、コマンド実行、コンテキストのコンパクションといった設定をそうしたオブジェクトへ移していく作業で占められている。

## 機能

**エージェントループの制御。** ライフサイクルフックは、セッション、ターン、ツール呼び出し、コンテキストのコンパクションの前後で発火する。0.1.13 からは、ツール実行前のフックがツールの実行前にその引数を書き換えられるようになった。安全ポリシー（`policy.allow`、`policy.deny`、`policy.ask_user`）はどのツール呼び出しを先に進めるかを決め、MCP サーバーの設定を直接対象に指定することもできる。0.1.11 からは、スクリプトからの利用、バックグラウンドでの利用、ヘッドレスでの利用に適するよう、SDK のデフォルトの `AgentBehavior` が対話的ではなく自律的なものになり、0.1.18 からは対話的な `ASK_QUESTION` ツールがデフォルトのツールセットから外されている。

**ツールと委譲。** エージェントは、[[DefinedTerm/model-context-protocol]] のサーバー（stdio および streamable HTTP。旧来の SSE トランスポートは 0.1.2 で削除された）、組み込みの Web 検索（0.1.4）と URL 取得（0.1.6）、コマンド実行 ― `RunCommandConfig(enable_sandbox=True)` によって OS レベルのサンドボックス内で実行することもできる（0.1.16）― 、そしてタイマーや cron 形式のバックグラウンドジョブのための `schedule` ツール（0.1.18 からデフォルトで有効）を利用できる。サブエージェントは静的に宣言でき（0.1.5）、独自の指示とツールの許可リスト（0.1.8）、独自のカスタムツール（0.1.15）、そして 0.1.18 からは独自のモデルを与えることができる。

**ローカルモデル。** 0.1.6 から、SDK はローカルモデルを相手にエージェントを実行できるようになった。LiteRT-LM を介した Gemma モデル向けの `LiteRTAgentConfig` と、Ollama や LM Studio といった OpenAI 互換エンドポイント向けの `LocalOpenAIAgentConfig` である。0.1.7 では MCP とサブエージェントのサポートがこれらのバックエンドにも拡張され、0.1.16 では小規模なローカルモデル向けの `.lightweight()` プリセットが続き、0.1.18 ではローカルモデルのサポートが正式なものとして発表された。

そのサポートに関する Google の発表（[[BlogPosting/introducing-support-for-local-ai-models-in-the-antigravity-sdk]]、2026 年 9 月 23 日）は、最初のモデルとして LiteRT 上の Gemma 4 26B A4B を挙げ、24GB を超える VRAM またはユニファイドメモリを備えたマシンを推奨し、`LocalOpenAIAgentConfig` を通じて利用できる OpenAI 互換サーバーとして Ollama、LM Studio、vLLM を挙げている。エージェントをローカルで実行する理由としては、コスト（API 料金やレート制限がない）、プライバシー（コードとリクエストがマシンの外に出ない）、オフラインでの耐障害性、クラウドとローカルを組み合わせたハイブリッドなワークフローが挙げられている。主要なデモンストレーションは、発表が Architect-Builder パターンと呼ぶものである。クラウドの Gemini モデルがファイル名とタスクの説明だけからタスクを計画・分解し、複数のローカルの Gemma インスタンスがデバイス上でコードを監査し、パッチを当て、テストするため、ソースコードはクラウドに一切送られない。

**運用上の制御。** `BudgetConfig`（0.1.11）はセッションのトークン数、ターン数、コストに上限を設け、`StopReason` はターンが終了した理由を報告する。`CompactionConfig`（0.1.17）は会話履歴がコンパクションされるトークンのしきい値を設定する。OpenTelemetry によるトレーシング（0.1.5）は、セッション、ターン、ステップ、ツールのイベントをスパンに対応付ける。0.1.18 では評価用のプリセット `AgentConfig.eval()` が追加された。チェンジログはこれを、コアとなるコーディング評価のための、標準化されたベンチマーク対応の設定と説明している。

## 採用とエコシステム

SDK は Gemini Developer API または Vertex AI に対して認証を行い、API キーを用いる Vertex AI Express モードにも対応しており、カスタムのベース URL やエンタープライズゲートウェイを経由させることもできる。デフォルトのモデルは Google の Gemini Flash のリリースに追随してきた ― 0.1.8 からは `gemini-3.6-flash`、0.1.11 からは `gemini-3.7-flash`、0.1.16 からは `gemini-3.8-flash` である。Windows のサポートは 0.1.2 で、Alpine Linux 向けの musllinux wheel は 0.1.15 で追加された。

Google Codelabs のチュートリアル（[[HowTo/ai-assisted-code-review-with-antigravity-cli-and-sdk]]）は、CI の中でヘッドレスに使われる SDK を示している。チュートリアルは、`google-antigravity` パッケージとしてインストールされる SDK を、Antigravity CLI と同じエージェントランタイムを Python ライブラリとして提供するものと説明し、現時点では Python でのみ利用可能だと述べている。チュートリアルはバージョン 0.1.7 に固定し、`LocalAgentConfig` から読み取り専用のコードレビューエージェントを構築する。その構成は、`policy.deny_all()` の後にファイル読み取り用ツール、コマンド実行、`finish` に対する `policy.allow` を続けるもの、`git` で始まらないコマンドをすべて拒否する `pre_tool_call_decide` フック（チュートリアルはこれを、ポリシーの上に重ねる第 2 の強制レイヤーとして示している）、ツールの結果をログに記録する `post_tool_call` フック、`skills_paths` を通じて読み込まれるエージェントスキル ― CLI が `.agents/skills/` から読み込むのと同じスキルファイルを、別の読み込み機構で読み込む ― 、そしてエージェントに構造化された指摘事項を返させる Pydantic の `response_schema` である。認証には、`GEMINI_API_KEY` が設定されていればそれを用い、そうでなければ Application Default Credentials を通じて Vertex AI にフォールバックする。そのうえでエージェントは各プルリクエストに対して GitHub Actions のワークフローによって実行され、指摘事項がコメントとして投稿される。
