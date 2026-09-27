---
title: "Cline"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, コーディングエージェント, コーディングツール, オープンソース, CLI, MCP]
translated_from: ".wikicommit/entity/en/SoftwareApplication/cline.md"
source_commit: "abe7dbaa9cb573068b927bda52cc565d6ba058e6"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Cline Bot Inc. によるオープンソースのコーディングエージェント。1 つの共通エージェントエンジンの上で VS Code 拡張機能、JetBrains プラグイン、CLI、デスクトップアプリとして動作し、そのエンジンはカスタムエージェントを構築するための SDK としても公開されている。"
  applicationCategory: "コーディングエージェント"
  author: "Cline Bot Inc."
---

Cline は、Cline Bot Inc. が Apache 2.0 ライセンスで公開しているオープンソースのコーディングエージェントであり、
自らを「IDE、ターミナル、デスクトップで動くオープンソースのコーディングエージェント（the open source coding agent in your IDE, terminal, & desktop）」と称している。
1 つのエージェントコアを共有するいくつかの形態で提供されている。VS Code 拡張機能、JetBrains 系 IDE 向けのプラグイン、
対話的にも完全なヘッドレスでも実行できるコマンドラインインターフェース、そして macOS と Windows 向けのネイティブデスクトップアプリである。
同じエンジンは、カスタムエージェントや連携機能を構築するための Node.js SDK としても公開されている。
リポジトリには SDK、CLI、VS Code 拡張機能、デスクトップアプリが含まれているが、共通エージェントコアと通信する
JetBrains プラグインはオープンソース化されていない。

## 機能

Cline はプロジェクトの構造を読み取り、複数のファイルにまたがる協調した変更を行う。その際にリンターやコンパイラの
エラーを監視し、インポートの欠落や型の不一致といった問題を修正できるようにしている。IDE クライアントでは、
各編集が差分として表示され、開発者はそれをレビュー、修正、あるいは取り消すことができる。また変更はチェックポイントで
追跡されるため、エージェントの作業を元に戻すことができる。ターミナルでシェルコマンドを実行してその出力を監視し、
開発サーバーのような長時間動き続けるプロセスについては、バックグラウンドで作業を続けながら新しい出力が現れるたびに反応する。

作業は、Cline がコードベースを調査し、確認のための質問をし、戦略を立てる **Plan モード** と、その計画を実行する
**Act モード** に分かれている。デフォルトでは、すべてのファイル編集とターミナルコマンドに開発者の承認が必要であり、
README はこれを開発者が主導権を保つための方法として示している（[[DefinedTerm/human-in-the-loop]]）。自動承認の
トグルを使えば、代わりに自律的に実行させることもできる。コーディング規約、アーキテクチャの慣例、デプロイ手順、
テスト要件といったプロジェクト固有のルールは `.clinerules` ファイルに記述され、CLI と両方の IDE クライアントが
自動的に読み込む。また、スキルによってモデルは特定のルールを必要なときにだけ読み込むことができる。

Cline は特定のモデルプロバイダーに縛られない。README には、Anthropic、OpenAI、Google のモデル、OpenRouter、
Vercel AI Gateway、AWS Bedrock、Azure と GCP Vertex、Cerebras と Groq、Ollama や LM Studio を介したローカルモデル、
そして任意の OpenAI 互換 API が挙げられている。拡張はプラグインを通じて行われ、プラグインは SDK を使って、ロギング、
監査、ポリシーの強制といった目的のためのツールやライフサイクルフックを登録する。あるいは
[[DefinedTerm/model-context-protocol]] サーバーを通じて拡張することもでき、CLI はこれを `cline mcp` で管理する。

単一のセッションを超えた機能として、README は次のものを説明している。マルチエージェントチームでは、
コーディネーターエージェントが作業をサブタスクに分割し、それぞれ独自のツールとコンテキストを持つ専門エージェントに
委任する。チームの状態はセッションをまたいで保持される。スケジュール型エージェントは、どのターミナルセッションとも
独立して cron スケジュールで実行され、毎日のプルリクエストの要約のような定期的なジョブに使われる。コネクタを使うと、
ユーザーは Telegram、Slack、Discord、Google Chat、WhatsApp、Linear からエージェントと対話でき、各会話スレッドが
1 つのエージェントセッションに対応する。ヘッドレス CLI はパイプによる入力を受け付け、JSON を出力できるため、
スクリプトや CI/CD パイプラインで利用できる。

## 採用とエコシステム

VS Code 拡張機能は Visual Studio Marketplace で、JetBrains プラグインは JetBrains Marketplace で配布されており、
後者は IntelliJ IDEA、PyCharm、WebStorm、GoLand をはじめとする JetBrains 系 IDE をカバーしている。CLI は npm から
`cline` として、SDK は `@cline/sdk` としてインストールできる。デスクトップアプリは Bun のサイドカーと Next.js の
インターフェースを備えた Tauri シェルとして構築されており、ユーザーは任意のフォルダでエージェントセッションを実行し、
ルーティンをスケジュールし、モデル、プラグイン、MCP サーバーを管理できる。
