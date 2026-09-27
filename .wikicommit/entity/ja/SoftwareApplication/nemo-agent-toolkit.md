---
title: "NVIDIA NeMo Agent Toolkit"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, エージェントツーリング, エージェントフレームワーク, オープンソース]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/nemo-agent-toolkit.md"
source_commit: "abe7dbaa9cb573068b927bda52cc565d6ba058e6"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AI エージェントのチームを接続・最適化するための、NVIDIA によるオープンソースの Python ライブラリ。既存のエージェントフレームワークを置き換えるのではなくそれらと併用し、プロファイリング、オブザーバビリティ、評価、最適化のための計測機能を追加する。"
  applicationCategory: "エージェントの計測・最適化ライブラリ"
  author: "[[Organization/nvidia]]"
---

NVIDIA NeMo Agent Toolkit は、AI エージェントのチームを接続・最適化するための [[Organization/nvidia]] によるオープンソースライブラリで、Apache 2.0 ライセンスで公開され、PyPI から `nvidia-nat` としてインストールする。フレームワーク非依存であり、エージェントフレームワークを置き換えるのではなく、それらと並行して動作する。README では [[SoftwareApplication/langchain]]、LlamaIndex、[[SoftwareApplication/crewai]]、Microsoft Semantic Kernel、Google の [[SoftwareApplication/agent-development-kit]] に加え、独自のエンタープライズ向けフレームワークや単純な Python エージェントも挙げられている。そのうえで、これらを使って構築したエージェントの観測、プロファイリング、最適化に必要な計測機能を追加する。

## 機能

ワークフローは、ツール（関数）、LLM、ワークフローの種類を指定した YAML 設定ファイルで宣言し、`nat` コマンドラインツールで実行する。README の入門例は、Wikipedia 検索ツールを与えた [[DefinedTerm/react-prompting]] エージェントである。コンポーネントは一度作って再利用することを想定しており、構築済みのエージェント、ツール、ワークフローはカスタマイズできる。また、組み込みのチャットインターフェースを使って、開発者はエージェントと対話し、出力を可視化し、ワークフローをデバッグできる。

実行時のエージェントを理解するために、このツールキットはワークフロー全体をエージェント単位から個々のトークン単位までプロファイリングしてボトルネックを特定し、トークン効率を分析する。また、本番環境での実行フローをトレースするためのオブザーバビリティを提供し、LangSmith のトレースにもネイティブに対応している。エージェントの改善のためには、オフライン評価システム、最適な設定とプロンプトを探索するハイパーパラメーター・プロンプト最適化機能、特定のエージェント向けに LLM を強化学習でファインチューニングする機能、大規模環境でのエージェント性能を高めるための NVIDIA Dynamo との実験的な統合、そして Agent Performance Primitives を提供する。Agent Performance Primitives は、並列実行、投機的分岐、ノード単位の優先度ルーティングによって、LangChain、CrewAI、Agno といったグラフベースのフレームワークを高速化する。

プロトコル面では、[[DefinedTerm/model-context-protocol]] のツールをエージェントに統合したり、ツールやエージェントを MCP サーバーとして公開したりでき、認証付きの分散エージェントのチームを構築するための [[DefinedTerm/agent2agent-protocol]] にも対応している。さらに、そのワークフローの構築、評価、最適化、観測について AI コーディングエージェントにタスク固有のガイダンスを与えるスキルと、公開プラグイン API も提供しており、サードパーティはこの API を使ってリポジトリ外で保守される統合を構築する。

`nat` ツールには、オプトイン方式のテレメトリーが含まれている。最初の対話的なコマンドで一度だけ同意プロンプトが表示され、既定値は「はい」である。一方、CI、cron ジョブ、パイプでつないだスクリプトなどの非対話的なコンテキストでは、環境変数で明示的に有効にしない限りデータは一切送信されない。各イベントにはコマンド名、その結果、所要時間と終了コード、例外が発生した場合はそのクラス名、Python のバージョンが記録される。README は、コマンド引数、ワークフロー名・関数名・モデル名、設定内容、ファイルパス、個人を特定できる情報は一切収集しないと明記している。

## 採用とエコシステム

README は、Google ADK と Microsoft AutoGen のフレームワーク対応について Synopsys を、評価・テレメトリーシステムへの貢献について W&B Weave チームをクレジットしており、プラグイン API 上に構築された外部保守のプラグインとして Tavily、Redis、ATR を挙げている。公表されているロードマップには、スタンドアロンの評価ハーネス、さらなるプログラミング言語への対応、既存エージェントへのスキルとサンドボックスの追加、自己改善型エージェントを支えるためのメモリインターフェースの改善が含まれる。
