---
title: "AGENTPI"
type: "schema:Dataset"
lang: ja
tags: []
translated_from: ".wikicommit/entity/en/Dataset/agentpi.md"
source_commit: "fed0100a95b9cbca3a6a11c43d68e28bc873bdea"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "動的でコンテキストに依存するタスクにおいて、コンテキストを考慮したプロンプトインジェクション攻撃のもとでの LLM エージェントの実行の完全性を評価するために明示的に設計された最初のベンチマーク。4 つのタスクドメイン（Banking、Travel、Workspace、Slack）にわたる 5 つのコンテキスト考慮型の攻撃ベクトルをカバーし、プロンプトインジェクションの全体像に関する SoK 論文で導入された。"
  creator: ["Peiran Wang", "Xinfeng Li", "Chong Xiang", "Jinghuai Zhang", "Ying Li", "Lixia Zhang", "Xiaofeng Wang", "Yuan Tian"]
---

AGENTPI は、[[ScholarlyArticle/landscape-of-prompt-injection-threats-in-llm-agents]] で導入されたベンチマークであり、コンテキストを考慮したプロンプトインジェクション攻撃のもとでの LLM エージェントの実行の完全性を評価するために設計されている。ここでいう攻撃とは、エージェントの行動がユーザーの最初のプロンプトによって完全に決まるのではなく、実行時の環境の観測に依存しなければならない、動的でコンテキスト依存のタスクを悪用するものである。

## 内容

このベンチマークは 200 の評価サンプルで構成され、5 つの攻撃ベクトルを 4 つのタスクドメインに適用したグリッドとして編成されており、20 通りの組み合わせのそれぞれに 10 個の固有サンプルがある。5 つの攻撃ベクトルは、アクションの切り替え、パラメータの操作、分岐の逸脱、推論の破壊、委譲の悪用である。攻撃は 4 つの異なる環境（Banking、Travel、Workspace、Slack）でテストされ、これらのドメイン全体で 66 の固有ツールをシミュレートすることで、現実世界のエージェントエコシステムに近づけ、防御が単一のシナリオではなく多様な API やロジック構造に対して評価されるようにしている。AGENTPI を特徴づけるのはそのコンテキストの複雑さである。ペイロードが注入されるツールの観測結果の平均長はおよそ 280 トークンであり、ベンチマークは短い文字列だけでなく、相当量の構造化データ（JSON やログなど）に対してエージェントが注意を維持できるかを評価する。AGENTPI の評価指標は多次元的で、攻撃成功率（ASR）、攻撃のない条件下での有用性、時間コスト、トークンコストをカバーする。

## 出自

AGENTPI は UCLA、NTU、NVIDIA の研究者によって作成され、LLM エージェントにおけるプロンプトインジェクションの脅威に関する体系的文献レビューと分類体系を扱う同じ論文の一部として導入された。

## 利用

[[ScholarlyArticle/landscape-of-prompt-injection-threats-in-llm-agents]] は AGENTPI を用いて、テキストレベルと実行レベルのカテゴリにまたがる 9 つの防御構成を GPT-4o-mini に対して実証的に評価し、それぞれについて攻撃成功率、有用性、計算コストのトレードオフを報告している。
