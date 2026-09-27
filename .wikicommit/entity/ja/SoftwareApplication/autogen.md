---
title: "AutoGen"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェント, マルチエージェント, オーケストレーション, エージェントツーリング]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/autogen.md"
source_commit: "4b83a0390f0437f8f63f9399a1db3e12e1ace784"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "ロールを担う複数のエージェントがメッセージを交換して答えに到達する、マルチエージェントの会話オーケストレーションフレームワーク。文書化されたパターンには、ソルバーエージェントが複数ラウンドにわたって議論し、アグリゲーターが多数決で結果を確定するディベート構成が含まれる。Microsoft は 2025 年にこれを Semantic Kernel と統合して Microsoft Agent Framework とした。"
  applicationCategory: "エージェントオーケストレーションフレームワーク"
  featureList: "マルチエージェントの会話の統一的なオーケストレーション、ソルバーエージェントとアグリゲーターエージェントによるディベートパターン、最終ラウンドの出力に対する多数決、RoundRobin 会話モード、各エージェントの判断をログに記録するためのコールバック関数"
---

AutoGen は、LLM で駆動される複数のエージェント間の会話を統一的にオーケストレーションするフレームワークである。[[SoftwareApplication/langgraph]] がエージェントをグラフとしてつなぎ、[[SoftwareApplication/crewai]] がエージェントをロールを担うチームとして編成するのに対し、ここで示される説明における AutoGen の中心的な発想は会話そのものである。エージェントにはロールが与えられ、結果に到達するまで互いに対話する。

## 機能

ソースがロール分離の実例として挙げているのは旅行計画の構成であり、`planner_agent` が初期計画を作成し、`language_agent` が言語面の助言を提供し、`travel_summary_agent` が複数の視点を最終計画に集約する。このうちソースは、1 つ目を [[DefinedTerm/llm-based-multi-agent-system]] の Planner ロールに、2 つ目を Reviewer ロールに対応づけている。Orchestrator ロールについては、この例ではなく別のフレームワークを用いて説明している。

エージェント間の意見の不一致に対して文書化されている対処法は **ディベート** パターンであり、エージェントが複数ラウンドにわたって立場を交換し、互いを修正する。ソルバーエージェントが答えを提案し、アグリゲーターエージェントがそれらを集め、最終ラウンドにおけるソルバーの出力に対する **多数決** で結果を確定する。ソースはこれを、マルチエージェントシステム一般で利用できる 3 つの調停戦略の 1 つとして提示しており、残りの 2 つは信頼度で重み付けした投票と信頼値に基づくルーティングである。AutoGen が文書化しているとソースが述べているのは多数決である。

会話の構造については、ソースは **RoundRobin** モードを挙げている。またトレーサビリティについては、AutoGen のコードでコールバック関数を使って各エージェントの判断の詳細を統一ログに出力でき、実行の推論を事後に突き合わせられると記している。

## 採用とエコシステム

ソースは、**Microsoft が 2025 年に AutoGen を Semantic Kernel と統合して [[SoftwareApplication/microsoft-agent-framework]] とした** ことを記録している。これにより、同社が 2 つのマルチエージェントフレームワークを並行して保守していた期間は終わった。ソースはこの統合を、この分野が機能を競い合う段階から、実験的なプロジェクト間で移行を繰り返すのではなく、チームが依存してもよいと考える少数のプロジェクトへと収束する段階に移ったことのシグナルと読んでいる。

## 関連用語

- [[SoftwareApplication/microsoft-agent-framework]] — AutoGen と Semantic Kernel の統合先
- [[DefinedTerm/llm-based-multi-agent-system]] — このフレームワークが調整する構成
- [[SoftwareApplication/langgraph]] — 同じソースが比較しているグラフ構造の代替
- [[SoftwareApplication/crewai]] — 同じソースが比較しているロールベースの代替
