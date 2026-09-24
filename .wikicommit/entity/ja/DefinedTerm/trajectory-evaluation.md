---
title: "軌跡評価（Trajectory Evaluation）"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/trajectory-evaluation.md"
source_commit: "c6bf44a9d0262400c75a0abf7dee6a8fbb53ff80"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "AI エージェントが結果に至るまでにたどった経路、すなわちツール呼び出しと推論が妥当であったかどうかを判定すること。最終結果が正しいかどうかだけを判定する出力評価とは区別される。"
---

軌跡評価は、決定論的なテストでは完全にはカバーされないエージェントの作業を検証するために、引用されている Google のホワイトペーパーが用いる 2 つの仕組みのうちの 1 つである。これは、エージェントが結果に至るまでにたどった経路、すなわちツール呼び出しと推論が妥当であったかどうかを問うものである。最終結果そのものが正しいかどうかだけを問う出力評価とは区別される。

## 用法

この区別は、両方の仕組みを併用すべき理由として示されている。正しく見えるがチェックを省略した回答は、明らかに壊れている回答よりも危険だとされる。出力評価だけではそれを合格させてしまうからである。ソースは、一回限りのデモではなくこの水準で評価の基準を設定することを、エージェントが一度は動くと示すことと、確実に動くと示すこととの違いとして位置づけている。

## 関連用語

[[BlogPosting/new-sdlc-vibe-coding]], [[DefinedTerm/llm-as-a-judge]]
