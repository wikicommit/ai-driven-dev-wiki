---
title: "Version Controlled Resolution（VCR）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/version-controlled-resolution.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている監査可能な成果物。人間はこれを通じて Consultation Request Pack または Merge-Readiness Pack に正式に応答し、それを解決する。トレーサビリティを保つため、対象となる成果物に明示的にリンクされる。"
---

Version Controlled Resolution（VCR）は、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で導入された [[DefinedTerm/structured-agentic-software-engineering]]（SASE）において、エージェントの [[DefinedTerm/consultation-request-pack]]（CRP）または [[DefinedTerm/merge-readiness-pack]]（MRP）に人間が応答するための成果物である。各 Resolution は対象となる成果物に明示的にリンクされ、トレーサビリティを保つとともに下流での監査と学習を可能にする。また、[[DefinedTerm/agentic-guidance-engineering]]（AGE）の活動の成果として作成される。

## 用法

論文は VCR を、非公式なチャットのやり取りではなく、構造化されバージョン管理された対話における人間側の成果物として位置づけている。人間は [[DefinedTerm/briefingscript]]、[[DefinedTerm/loopscript]]、[[DefinedTerm/mentorscript]] で作業を開始し、エージェントは CRP または MRP で応答し、人間は VCR でループを閉じる。これらの成果物へのバージョン管理された更新が、時間の経過に伴う明確化とフィードバックを記録し、タスク、プロセス、チームの規範についての共通理解を最新の状態に保つ。

## 関連用語

[[DefinedTerm/consultation-request-pack]], [[DefinedTerm/merge-readiness-pack]], [[DefinedTerm/agentic-guidance-engineering]]
