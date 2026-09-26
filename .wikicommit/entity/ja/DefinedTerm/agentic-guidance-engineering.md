---
title: "Agentic Guidance Engineering（AGE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agentic-guidance-engineering.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されたエンジニアリング活動のひとつで、エージェントが生成した Consultation Request Pack と Merge-Readiness Pack を人間がレビューし応答する際の構造化された役割を統制し、人間を受動的な承認者から、必要に応じて的を絞って相談に応じるコンサルタントへと引き上げるもの。"
---

Agentic Guidance Engineering（AGE）は、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で [[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として提案された、構造化されたエンジニアリング活動のひとつである。[[DefinedTerm/briefing-engineering]] が作業を開始させるのに対し、AGE は、人間がエージェントの生成した成果物や確認要求をどのようにレビューし応答するかを統制し、人間の専門性が最も大きな価値を生む箇所に的確に介入させる。

## 用法

論文は AGE を人間のエンジニア — タスクの当初の発案者、または領域の専門家 — に割り当て、[[DefinedTerm/agent-command-environment]]（ACE）の中で行われるものとしている。論文によれば ACE は、[[DefinedTerm/consultation-request-pack]]（CRP）をトリアージし、[[DefinedTerm/merge-readiness-pack]]（MRP）を監査し、構造化された解決を発行するための、受信箱のようなインターフェースを提供する。AGE はこれら 2 種類のエージェント生成成果物を入力とし、それぞれに対して [[DefinedTerm/version-controlled-resolution]]（VCR）を生成する。VCR は、トレーサビリティを保ち、下流での監査と学習を可能にするために、対象とする成果物に明示的に紐づけられる。

## 関連用語

[[DefinedTerm/consultation-request-pack]]、[[DefinedTerm/merge-readiness-pack]]、[[DefinedTerm/version-controlled-resolution]]
