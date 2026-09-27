---
title: "AutoDev"
type: "schema:SoftwareApplication"
lang: ja
tags: [コーディングエージェント, エージェントツーリング, サンドボックス化, マルチエージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/autodev.md"
source_commit: "029a1c18064c79f7a24b408c62abfa180a4f512c"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AI 駆動による自律的なソフトウェア開発のための Microsoft のフレームワーク。AI エージェントが、ユーザーの許可したコマンドに限定された Docker コンテナ内で、ファイルの編集、コードの取得、ビルド、実行、テスト、git 操作を行い、ユーザーが定義した目標を達成する。"
  applicationCategory: "ソフトウェアエンジニアリングのための自律型 AI エージェントフレームワーク"
  featureList: "コマンドパーサーと出力オーガナイザーを備えた Conversation Manager、Tools Library（ファイル編集、取得、ビルドと実行、テストと検証、git、コミュニケーション）、ラウンドロビン・トークンベース・優先度ベースの協調を備えた Agent Scheduler、Docker ベースの Evaluation Environment、YAML で設定するルール・アクション・パーミッション"
  author: "[[Organization/microsoft]]"
---

AutoDev は、ソフトウェアエンジニアリングのタスクを自律的に計画・実行するために設計された、Microsoft による完全自動の AI 駆動ソフトウェア開発フレームワークである。ユーザーが目標（たとえば特定のメソッドをテストすること）を定義すると、AutoDev の AI エージェントはリポジトリ内でアクションを実行してそれを追求する。テストファイルを書き、それを実行し、失敗ログを読み、さらにコンテキストを取得し、ファイルを修正し、テストが通るまで再実行する。開発者の介入は目標の設定だけである。

これを導入した論文 [[ScholarlyArticle/autodev-automated-ai-driven-development]] は、AutoDev を [[SoftwareApplication/github-copilot]] のような IDE に統合された AI コーディングアシスタントと対比させて位置づけている。論文によれば、そうしたアシスタントは主にチャットインターフェースでコードを提案するだけで、テストの実行や出力の検証は開発者自身に委ねている。論文は AutoDev を、[[SoftwareApplication/autogen]] を会話管理の先まで拡張し、エージェントがリポジトリに対して行動できるようにしたものであり、かつ LLM 非依存で、異なるサイズやアーキテクチャのモデルが 1 つのタスクで協調できるものだと説明している。

## 機能

ユーザーはまず YAML ファイルでルールとアクションを設定し、特定のコマンドを有効化または無効化するとともに、エージェントの数、その責務、利用可能なアクションを定義する。たとえば「Developer」エージェントと「Reviewer」エージェントといった具合である。Conversation Manager は会話を初期化・維持し、各エージェントの応答をコマンドと引数に解析し、それをユーザーのパーミッションと照合し、各結果の構造化された要約を会話に追加する。エージェントが `stop` を発行したとき、ユーザー定義の反復回数またはトークンの上限に達したとき、あるいは問題が検出されたときに会話を終了する。Agent Scheduler は、ラウンドロビン、トークンベース、優先度ベースのいずれかの協調方式を用いて、次にどのエージェントが行動するかを決める。

Tools Library は、低レベルのコマンドを単純なコマンドの背後に抽象化する。対象は、ファイル編集（`write`、`edit`、`insert`、`delete` で、行範囲の単位まで指定可能）、`grep`、`find`、`ls` から類似スニペットの埋め込みベースの取得までを含む取得、ビルドと実行（`build`、`run`）、テストと検証（`test`、`syntax`、リンターやバグ検出ツール）、ローカルコミットのみを許可するといったきめ細かなパーミッションを伴う git 操作、そしてコミュニケーションコマンドの `talk`、`ask`、`stop` である。すべてのコマンドは Docker ベースの Evaluation Environment 内で実行され、標準出力とエラーが会話に返される。

## 採用とエコシステム

パイロットスタディでは、開発者は VS Code で会話を見ながら、AutoDev を CLI コマンドとして使用した。エージェントがユーザーにフィードバックを求めることを可能にする `ask` コマンドは、このスタディの中で開発者の要望を受けて追加された。著者らは、AutoDev をチャットボット体験として IDE に統合し、さらに CI/CD パイプラインや PR レビュープラットフォームにも統合して、開発者がタスクやイシューを AutoDev に割り当て、その結果を PR システムでレビューできるようにすることを計画している。
