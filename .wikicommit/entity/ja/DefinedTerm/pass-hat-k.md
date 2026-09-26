---
title: "pass^k"
type: "schema:DefinedTerm"
lang: ja
aliases: ["pass-hat-k"]
tags: [エージェント評価, 評価]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/pass-hat-k.md"
source_commit: "02f7d23719e4ec300fc997d58e966c19037dfd22"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "あるタスクの k 回の試行がすべて成功する確率を示す評価指標。エージェントがどれだけ一貫して動作するかを測るために用いられる。"
---

pass^k は、あるタスクの *k 回すべての* 試行が成功する確率を測る評価指標である。より多くの試行にわたって一貫性を求めることはより高いハードルになるため、*k* が大きくなるにつれてスコアは下がる。*k* = 1 のときは試行ごとの成功率に等しい。試行ごとの成功率が 75% のエージェントの場合、3 回の試行すべてに合格する確率は (0.75)³ ≈ 42% である。

## 用法

[[BlogPosting/demystifying-evals-for-ai-agents]] は、実行ごとに振る舞いが変わるエージェントの非決定性を捉える方法として、[[DefinedTerm/pass-at-k]] と並べて pass^k を示している。同記事は、ユーザーが毎回信頼できる振る舞いを期待する顧客対応のエージェントでは pass^k がとりわけ重要だと論じ、一貫性が欠かせないエージェントにはこれを推奨する一方、1 回の成功で十分なツールには pass@k が適しているとしている。2 つの指標は *k* = 1 では一致し、試行が増えるにつれて乖離する。*k* = 10 では、pass@k が 100% に近づく一方で pass^k は 0% に向かって下がる。

この指標の定義について、同記事は、小売サポートや航空券予約といったドメインでのマルチターンの会話をシミュレートするベンチマークである [[Dataset/tau-bench]] について引用しているのと同じ論文にリンクしている。

## 関連用語

[[DefinedTerm/pass-at-k]], [[Dataset/tau-bench]]
