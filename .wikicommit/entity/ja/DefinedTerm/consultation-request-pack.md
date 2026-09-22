---
title: "Consultation Request Pack（CRP）"
type: "schema:DefinedTerm"
lang: ja
tags: [sase]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/consultation-request-pack.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-22"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている構造化された成果物。エージェントが判断や不確実性を人間の専門家へ正式にエスカレーションするために生成するもので、その場限りの人間への相談を追跡可能なチームの成果物へと変える。"
---

Consultation Request Pack（CRP）とは、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で導入された [[DefinedTerm/structured-agentic-software-engineering]]（SASE）において、エージェントが先へ進むために人間の入力を必要とするときに生成する成果物である。これは有効な [[DefinedTerm/briefingscript]] によって文脈づけられ、[[DefinedTerm/loopscript]] や [[DefinedTerm/mentorscript]] の規則によって発火しうる。エージェントが遭遇した具体的な不確実性ないし判断点を文書化するものである。

## 用法

[[DefinedTerm/agent-command-environment]]（ACE）が各 CRP を振り分け、提示し、記録する。そこでは対象となる人間が呼び出し可能な専門知の窓口として扱われる一方、説明責任に必要な文脈は保たれる。同論文の付録にある具体例では、エージェントが、BriefingScript で指定された Redis バックエンドと、重要度の高い決済エンドポイントにおけるレプリケーション遅延についての既知の「落とし穴」との衝突をエスカレーションしており、判断を下す人間に対して構造化された選択肢（それぞれに利点、欠点、見積もり工数を添えたもの）、エージェント自身の推奨とその理由、そしてエスカレーション先（たとえば「テックリードないしアーキテクトの役割」）を提示している。人間は CRP に対して [[DefinedTerm/version-controlled-resolution]]（VCR）で応答し、これは下流での監査と学習のために追跡可能性を保つべく、対応する CRP へ明示的に紐づけられる。

## 関連用語

[[DefinedTerm/version-controlled-resolution]]、[[DefinedTerm/agentic-guidance-engineering]]、[[DefinedTerm/merge-readiness-pack]]
