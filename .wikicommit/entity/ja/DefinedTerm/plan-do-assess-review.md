---
title: "Plan-Do-Assess-Review（PDAR）"
type: "schema:DefinedTerm"
lang: ja
tags: [仕様駆動開発]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/plan-do-assess-review.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "人間と AI が計画し、開発エージェントが実装し、エージェントが自己評価し、人間がレビューするという反復的なタスクのライフサイクル。Product Requirement Prompt を中心に形式化されており、Structured Agentic Software Engineering のよりチームレベルのオーケストレーションの先駆けとして引用されている。"
---

Plan-Do-Assess-Review（PDAR）ループは、単一のエージェント型タスクのライフサイクルのための反復的なワークフローであり、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で論じられている。人間と AI が作業を計画し、開発エージェントがそれを実装し、エージェントが結果を自己評価し、人間がそれをレビューする。同論文は、これが [[DefinedTerm/product-requirement-prompt]]（PRP）と組み合わせて使われるのが一般的だと説明している。PRP は、目標、その根拠、受け入れ基準、厳選されたコンテキストをまとめた「minimum viable packet（最小限の実用パケット）」である。同論文は、この仕様駆動のパターンをすでに実践している業界のツールとして Amazon の [[SoftwareApplication/kiro]] を挙げている。

## 用法

同論文は PDAR を、場当たり的なエージェント型プロンプティングに秩序をもたらそうとする初期の重要な試みとして評価し、その構造化されテスト可能な意図は [[DefinedTerm/structured-agentic-software-engineering]]（SASE）自身が構造を重視する姿勢と合致すると述べている。同論文は PDAR を、一回限りのタスク実行に範囲が限られたものと位置づけている。PDAR はそれだけでは、継続的なメンタリング、エージェントのライフサイクルを通じた学習、タスク横断のトレーサビリティを確立しない。SASE はこれらを第一級の関心事として扱い、代わりに [[DefinedTerm/mentorscript]] や [[DefinedTerm/loopscript]] といったアーティファクトによって対処する。

## 適用される場面

同論文は PDAR を、自ら考案したプラクティスではなく既存の業界パターンとして提示しており、PRP による構造化は特に Amazon の Kiro のようなツールに由来するものとしている。そして自らの貢献を、PDAR の単一タスクのループを、チームレベルの N 対 N の人間とエージェントの協働へと拡張するものとして位置づけている。

## 関連用語

[[DefinedTerm/product-requirement-prompt]]、[[SoftwareApplication/kiro]]、[[DefinedTerm/agentic-loop-engineering]]
