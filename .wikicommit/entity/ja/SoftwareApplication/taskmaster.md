---
title: "Taskmaster"
type: "schema:SoftwareApplication"
lang: ja
tags: [コーディングツール, エージェントツーリング, MCP, CLI, 仕様駆動開発]
translated_from: ".wikicommit/entity/en/SoftwareApplication/taskmaster.md"
source_commit: "abe7dbaa9cb573068b927bda52cc565d6ba058e6"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "AI 駆動開発のためのタスク管理システム。プロダクト要求仕様書を解析して、AI コーディングアシスタントが計画・展開・順次実行できる構造化されたタスクへと変換する。AI エディタ内の MCP サーバーとして、または `task-master` コマンドラインツールとして動作する。"
  applicationCategory: "AI 駆動開発のためのタスク管理"
---

Taskmaster（Task Master とも表記され、npm では `task-master-ai` として公開されている）は、AI 駆動開発のためのタスク管理システムである。README は、任意の AI チャットで動作するように設計されており、特に [[SoftwareApplication/cursor]] とあわせて Claude で開発するために作られたものだと説明している。リポジトリの説明文はさらに、Cursor、Lovable、Windsurf、Roo などのツールにそのまま組み込めると付け加えている。Taskmaster はプロジェクトの要求を構造化されたタスクのリストに変換し、開発者の AI アシスタントはそれに基づいて計画を立て、タスクを分解し、1 つずつ実装していく。ドキュメントは Hamster のウェブサイトで公開されており、README は Hamster の他の製品へのリンクも掲載している。

## 機能

README が推奨するワークフローは、プロダクト要求仕様書（PRD）から始まる。「常に詳細な PRD から始めよ」というのがその指針であり、PRD が詳細であるほど生成されるタスクも良くなるという理由が述べられている。Taskmaster は PRD を解析してタスクにし、開発者はその後、次に取り組むべきタスクを尋ねたり、特定のタスクの実装への支援を求めたり、タスクをサブタスクに展開するよう依頼したりする。PRD なしで、チャットでの依頼から個々のタスクを直接作成することもできる。タスクは依存関係を持ち、タグの下に整理することができ、依存関係ごと、あるいは依存関係なしでタスクをタグ間で移動するコマンドも用意されている。research コマンドは、必要に応じてプロジェクトのコンテキストも加えて最新の情報を取得する。ドキュメントでは、タスクの複雑さの分析、チームでの共同作業、自動化のための loop コマンドも扱われている。

これらのコマンドのいくつかは LLM を呼び出すため、Taskmaster には少なくとも 1 つのプロバイダの設定が必要である。Taskmaster は 3 つのモデルの役割 ― メインモデル、リサーチモデル、そして他の 2 つのいずれかが失敗したときに使われるフォールバックモデル ― を区別しており、Anthropic、OpenAI、Google Gemini、Perplexity（リサーチ用として推奨されている）、xAI、OpenRouter などを API キー経由でサポートするほか、[[SoftwareApplication/claude-code]] と Codex CLI（[[SoftwareApplication/openai-codex]]）をそれぞれ自身のサインインを通じて、API キーなしで利用することもできる。

実行方法は 2 通りある。推奨されているのは、エディタに設定した [[DefinedTerm/model-context-protocol]] サーバーとして動かす方法である。README は Cursor、Windsurf、VS Code、Amazon Q Developer CLI 向けの設定パスと、Claude Code 向けの 1 行のインストール手順を示しており、設定後は開発者がエディタの AI チャットに話しかけることで Taskmaster を操作する（「Initialize taskmaster-ai in my project」「What's the next task I should work on?」）。もう 1 つは `task-master` コマンドラインツールで、`parse-prd`、`list`、`next`、`show`、`research` などのコマンドがあり、`init` ステップでは特定のエディタ向けのルールファイルをインストールすることもできる。

ツールのリストが大きいとコンテキストを消費するため、MCP サーバーはツールの選択的な読み込みをサポートしている。デフォルトでは 36 個のツールがすべて読み込まれ、README によればこれはおよそ 21,000 トークンに相当する。15 個のツールからなる `standard` セットと、7 個のツール（たとえば、タスクの取得、次のタスクの検索、タスクのステータス設定、PRD の解析、タスクの展開）からなる `core` セットを使えばこれを削減でき、カンマ区切りのカスタムリストも受け付ける。README は、新規ユーザーには standard セットを、大規模なプロジェクトには core セットを推奨している。

## 採用状況とエコシステム

Taskmaster は、Commons Clause 付きの MIT ライセンスのもとで提供されている。README の要約によれば、このツールはあらゆる目的で使用、改変、再配布でき、これを使って構築した製品を販売することもできるが、Taskmaster そのものを販売したり、ホスティングサービスとして提供したり、競合製品の基盤として使用したりすることはできない。
