---
title: "Product Requirement Prompt（PRP）"
type: "schema:DefinedTerm"
lang: ja
tags: [仕様駆動開発]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/product-requirement-prompt.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "エージェント型コーディングのタスクのための「最小実行可能パケット」としての仕様パターン。Goal & Why、What & Success Criteria、All Needed Context、Implementation Blueprint、Validation Loop の 5 つのセクションで構成され、Amazon の Kiro などの業界ツールがその実例を示している。"
---

Product Requirement Prompt（PRP）は、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で論じられている仕様のアーティファクトであり、タスクの目標、その根拠、受け入れ基準、そして厳選したコンテキストを、AI コーディングエージェントのための「最小実行可能パケット」としてまとめたものである。論文は、Amazon の [[SoftwareApplication/kiro]] などの業界ツールが、この仕様駆動開発のパターンをすでに実践していると述べている。

## 用法

論文によれば、PRP は典型的に 5 つのセクションで構成される。(1) Goal & Why は目的とビジネス上の価値を定める。(2) What & Success Criteria は検証可能な条件と不変条件によってスコープを定義する。(3) All Needed Context は、エージェントのコンテキストに過剰な負荷をかけることなく、関連するドキュメントと既知の落とし穴を厳選して盛り込む。(4) Implementation Blueprint は、低レベルの計画ではなく、戦略的な指針と制約を与える。(5) Validation Loop は受け入れテストの戦略を明文化する。PRP は [[DefinedTerm/plan-do-assess-review]]（PDAR）のループの中で用いられ、論文は PRP を SASE 独自の [[DefinedTerm/briefingscript]] と対応づけて、両者がともに構造化されテスト可能な意図を求めている点を指摘している。

## 関連用語

[[DefinedTerm/plan-do-assess-review]], [[SoftwareApplication/kiro]], [[DefinedTerm/briefingscript]]
