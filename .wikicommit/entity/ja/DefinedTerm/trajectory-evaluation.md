---
title: "軌跡評価"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/trajectory-evaluation.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "AI エージェントが結果に至るまでにたどった経路——そのツール呼び出しと推論——が妥当であったかを判断すること。最終結果が正しいかどうかだけを判断する出力評価とは区別される。"
---

軌跡評価とは、引用されている Google のホワイトペーパーが、決定論的なテストでは完全にはカバーされないエージェントの作業を検証するために用いる 2 つの仕組みのうちの 1 つであり、エージェントが結果に至るまでにたどった経路、すなわちそのツール呼び出しと推論が妥当であったかを問うものである。これは、最終結果そのものが正しいかどうかだけを問う出力評価とは区別される。

## 用法

この区別は、両方の仕組みを併せて用いるべき理由として提示されている。正しく見えるもののチェックを飛ばした回答は、明らかに壊れている回答よりも危険だとされる。出力評価だけではそれを通過させてしまうからである。ソースは、一度きりのデモではなくこの水準で評価の基準を設定することを、エージェントが一度は機能しうると示すことと、確実に機能すると示すこととの違いとして位置づけている。

## 関連用語

[[BlogPosting/new-sdlc-vibe-coding]]、[[DefinedTerm/llm-as-a-judge]]
