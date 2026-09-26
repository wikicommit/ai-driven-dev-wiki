---
title: "pass@k"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェント評価, 評価]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/pass-at-k.md"
source_commit: "02f7d23719e4ec300fc997d58e966c19037dfd22"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "エージェントやモデルが、あるタスクに対する k 回の試行のうち少なくとも 1 回正しい解を出す可能性を示す評価指標。"
---

pass@k は、エージェントがあるタスクに対する *k* 回の試行のうち少なくとも 1 回正しい解を得る可能性を測る評価指標である。試行が多いほど成功の機会も増えるため、*k* が大きくなるにつれてスコアは上がる。*k* = 1 のときは試行ごとの成功率に等しく、pass@1 が 50% であれば、モデルは評価のタスクの半分を最初の試行で成功させることを意味する。

## 用法

[[BlogPosting/demystifying-evals-for-ai-agents]] は、同じタスクがある実行では合格し次の実行では不合格になりうるというエージェント評価の非決定性に対処するための 2 つの指標の 1 つとして pass@k を示している。同記事は、コーディングでは主な関心がエージェントが最初の試行で解を見つけること、すなわち pass@1 にあることが多い一方、ほかのケースでは、多くの解を提案してもそのうち 1 つがうまくいけば許容されると述べている。同じ記事は、1 回の成功が重要なツールには pass@k を、一貫性が欠かせないエージェントにはその対となる [[DefinedTerm/pass-hat-k]] を推奨している。試行が増えるにつれて両者は乖離し、*k* = 10 では pass@k が 100% に近づく一方で pass^k は 0% に向かって下がる。

同記事はこの指標を評価結果の読み取りにも用いている。フロンティアモデルの場合、多数の試行にわたる合格率 0%（記事の例では pass@100 が 0%）は、エージェントの能力不足よりも、壊れたタスクの兆候であることが最も多いとされる。

## 関連用語

[[DefinedTerm/pass-hat-k]], [[DefinedTerm/trajectory-evaluation]]
