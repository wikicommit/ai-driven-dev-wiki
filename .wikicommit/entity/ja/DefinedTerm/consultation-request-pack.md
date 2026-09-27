---
title: "Consultation Request Pack（CRP）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/consultation-request-pack.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている構造化された成果物。エージェントが判断や不確実性を人間の専門家に正式にエスカレーションするために生成するもので、場当たり的な人間への相談を、追跡可能なチームの成果物へと変える。"
---

Consultation Request Pack（CRP）とは、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で導入された [[DefinedTerm/structured-agentic-software-engineering]]（SASE）において、エージェントが先に進むために人間の入力を必要とするときに生成する成果物である。CRP は有効な [[DefinedTerm/briefingscript]] によって文脈づけられ、[[DefinedTerm/loopscript]] や [[DefinedTerm/mentorscript]] のルールによって発動されることもある。CRP には、エージェントが直面した具体的な不確実性や判断のポイントが記録される。

## 用法

[[DefinedTerm/agent-command-environment]]（ACE）は各 CRP をルーティングし、提示し、記録する。その際、対象となる人間を呼び出し可能な専門知識のエンドポイントとして扱いつつ、説明責任に必要なコンテキストを保持する。論文の付録にある具体例では、エージェントが、BriefingScript で指定された Redis バックエンドと、重要度の高い決済エンドポイントにおけるレプリケーション遅延についての既知の「落とし穴」との矛盾をエスカレーションしている。エージェントは人間の意思決定者に対して、構造化された選択肢（それぞれに利点、欠点、見積もり工数が付く）、エージェント自身の推奨とその理由、そしてエスカレーション先（例：「テックリードまたはアーキテクトの役割」）を提示する。人間は CRP に対して [[DefinedTerm/version-controlled-resolution]]（VCR）で応答し、VCR は下流での監査や学習のための追跡可能性を保つため、それが対処する CRP に明示的に結びつけられる。

## 関連用語

[[DefinedTerm/version-controlled-resolution]]、[[DefinedTerm/agentic-guidance-engineering]]、[[DefinedTerm/merge-readiness-pack]]
