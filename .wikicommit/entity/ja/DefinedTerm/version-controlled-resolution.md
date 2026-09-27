---
title: "Version Controlled Resolution（VCR）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/version-controlled-resolution.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案された監査可能な成果物。人間はこれを通じて Consultation Request Pack または Merge-Readiness Pack に正式に応答し、それを解決する。追跡可能性を保つため、対象となる成果物に明示的に結びつけられる。"
---

Version Controlled Resolution（VCR）とは、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で導入された [[DefinedTerm/structured-agentic-software-engineering]]（SASE）において、人間がエージェントの [[DefinedTerm/consultation-request-pack]]（CRP）または [[DefinedTerm/merge-readiness-pack]]（MRP）に応答するための成果物である。各 Resolution は、それが対処する成果物に明示的に結びつけられ、追跡可能性を保つとともに、下流での監査や学習を可能にする。VCR は [[DefinedTerm/agentic-guidance-engineering]]（AGE）の活動の成果として生成される。

## 用法

論文は VCR を、非公式なチャットのやり取りではなく、構造化され、バージョン管理された対話における人間の側として位置づけている。人間は [[DefinedTerm/briefingscript]]、[[DefinedTerm/loopscript]]、[[DefinedTerm/mentorscript]] によって作業を開始し、エージェントは CRP または MRP で応答し、人間は VCR によってループを閉じる。これらの成果物に対するバージョン管理された更新が、時間の経過に伴う明確化やフィードバックを記録し、タスク、プロセス、チームの規範についての共通理解を最新の状態に保つ。

## 関連用語

[[DefinedTerm/consultation-request-pack]], [[DefinedTerm/merge-readiness-pack]], [[DefinedTerm/agentic-guidance-engineering]]
