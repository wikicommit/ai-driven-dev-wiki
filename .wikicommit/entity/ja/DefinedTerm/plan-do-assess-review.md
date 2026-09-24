---
title: "Plan-Do-Assess-Review（PDAR）"
type: "schema:DefinedTerm"
lang: ja
tags: [仕様駆動開発]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/plan-do-assess-review.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "人間と AI が計画し、dev-agent が実装し、エージェントが自己評価し、人間がレビューするという反復的なタスクのライフサイクル。Product Requirement Prompt を軸に定式化されており、Structured Agentic Software Engineering のよりチームレベルのオーケストレーションの先駆けとして引かれている。"
---

Plan-Do-Assess-Review（PDAR）ループは、単一のエージェント型タスクのライフサイクルのための反復的なワークフローであり、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で論じられている。人間と AI が作業を計画し、dev-agent がそれを実装し、エージェントが結果を自己評価し、人間がそれをレビューする。論文はこれを、[[DefinedTerm/product-requirement-prompt]]（PRP）——目標、根拠、受け入れ基準、厳選されたコンテキストを収めた「最小限の実用的なパケット（minimum viable packet）」——と組み合わせて使われるのが一般的なものとして説明しており、この仕様駆動のパターンをすでに示している業界のツールとして Amazon の [[SoftwareApplication/kiro]] を挙げている。

## 用法

論文は PDAR を、場当たり的なエージェント型のプロンプティングに秩序をもたらそうとする初期の重要な試みとして評価し、その構造化されテスト可能な意図は、構造を重視する [[DefinedTerm/structured-agentic-software-engineering]]（SASE）自身の姿勢と合致すると述べている。論文は PDAR を 1 回限りのタスク実行に範囲が限られたものとして位置づけている。それ自体では、永続的なメンタリング、エージェントのライフサイクルを通じた学習、タスク横断のトレーサビリティを確立しない。SASE はこれらを第一級の関心事として扱い、代わりに [[DefinedTerm/mentorscript]] や [[DefinedTerm/loopscript]] といった成果物によって対処する。

## 適用される場面

論文は PDAR を、自らが生み出した実践としてではなく既存の業界のパターンとして提示しており——PRP による構造化は特に Amazon の Kiro のようなツールに帰している——、自らの貢献を、PDAR の単一タスクのループをチームレベルの N 対 N の人間とエージェントの協働へと拡張するものとして位置づけている。

## 関連用語

[[DefinedTerm/product-requirement-prompt]], [[SoftwareApplication/kiro]], [[DefinedTerm/agentic-loop-engineering]]
