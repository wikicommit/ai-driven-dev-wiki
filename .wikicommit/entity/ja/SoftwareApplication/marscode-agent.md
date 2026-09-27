---
title: "MarsCode Agent"
type: "schema:SoftwareApplication"
lang: ja
tags: [コーディングエージェント, プログラム修復, マルチエージェント]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/marscode-agent.md"
source_commit: "90f235c19401779128f2c36166ba9e641fa1393d"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "ByteDance による、自動バグ修正のための LLM ベースのエージェントフレームワーク。ロールごとの複数のエージェントがコードの検索、計画、再現、編集、テストを行い、Issue に対するパッチを作成する。"
  applicationCategory: "自動バグ修正エージェントフレームワーク"
  featureList: "マルチエージェントの協働（Searcher、Planner、Reproducer、Programmer、Tester、Editor）、動的デバッグと静的修復のワークフロー、コードナレッジグラフによる検索、あいまい位置特定を備えた Language Server Protocol による検索、ファイル検索と grep 検索、AutoDiff によるコード編集、LSP による静的コード診断、Docker ベースのランタイムサンドボックス"
---

MarsCode Agent は、LLM を用いてソフトウェアコード中のバグを自動的に特定・修復する、ByteDance によるフレームワークである。
[[ScholarlyArticle/marscode-agent-ai-native-automated-bug-fixing]] で紹介されており、同論文はこれを、エージェントフレームワークを構築し、コードの検索、デバッグ、編集のための対話的なインターフェースとツールをエージェントに提供することで、エージェントがソフトウェアエンジニアリングのタスクの一部を担えるようにするものと説明している。

## 機能

作業は 6 つのロールに分担される。Searcher はコードナレッジグラフと Language Server Protocol を用いて Issue に関連するコード片を収集し、Planner はそれらを分析して Issue を動的デバッグと静的修復のいずれかのワークフローに分類する。Reproducer は再現スクリプトを作成してサンドボックス内で Issue が再現することを確認し、Programmer はコードを編集し、Tester は各バージョンを再現スクリプトに照らして確認し、Editor は静的修復のために複数の修復案を提示する。コードを編集できるのは Programmer と Editor のみ、リポジトリをリセットできるのは Programmer のみ、再現スクリプトを実行できるのは Reproducer と Tester のみである。動的デバッグでは、Docker コンテナ内に構築されたランタイムサンドボックスの中で、Issue が解決するまで Programmer と Tester が反復する。静的修復では、[[DefinedTerm/agentless]] に似たアプローチに基づき、1 回の LLM リクエストで複数の修正候補を生成し、AST で正規化したうえでマージして投票にかける。

検索のために、MarsCode Agent はコードナレッジグラフを構築する。そのノードは変数、関数、クラス、ファイルといったコードエンティティであり、エッジはファイル構造、関数呼び出し、シンボル参照を記録する。エージェントのクエリはグラフに対してエンティティ認識、埋め込みの類似度、キーワード検索を経て処理され、統合された候補が再ランキングされる。Language Server Protocol は、対象プロジェクト外の定義や参照についてグラフを補完するものであり、エージェントが与えたファイル名、行番号、識別子から LSP リクエストを組み立てるあいまい位置特定の機能を備えている。汎用的なファイル検索や grep も利用できる。

コードの編集は AutoDiff で記述される。これは Aider に着想を得た、git のコンフリクトマーカーに似た形式である。エージェントがファイルパス、元のコード、置き換え後のコードを与えると、ツールは元のコード片をファイル中で最も類似した箇所に照合して置き換え、インデントを調整し、unified diff を生成する。その後、各編集は変更の前後で LSP の静的診断によってチェックされ、Fatal または Error レベルの新たなエラーが現れた場合には、その診断結果がエージェントに返されてさらなる修正が行われる。

## 採用とエコシステム

このレポートは、[[Dataset/swe-bench]] の一部である SWE-bench Lite で MarsCode Agent を評価し、そのコード検索を CodeR、Moatless、Agentless など、公開されていて追跡可能な他のソリューションと比較している。著者らは、このフレームワークに関する今後の計画として、LLM の呼び出しコストの削減、ユーザーとエージェントの協働の改善、実際のユーザーのワークスペース内での動的デバッグのサポートなどを挙げている。
