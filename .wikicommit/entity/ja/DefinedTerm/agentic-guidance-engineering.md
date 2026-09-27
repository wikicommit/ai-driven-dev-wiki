---
title: "Agentic Guidance Engineering（AGE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
translated_from: ".wikicommit/entity/en/DefinedTerm/agentic-guidance-engineering.md"
source_commit: "f3cd768971749927e49083efe4fbd9f44cf27fb0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Structured Agentic Software Engineering（SASE）で提唱されているエンジニアリング活動で、エージェントが生成した Consultation Request Pack と Merge-Readiness Pack をレビューし、それに応答するという人間の構造化された役割を律するもの。これにより人間は、受け身の承認者から、必要に応じて的を絞って助言するコンサルタントへと引き上げられる。"
---

Agentic Guidance Engineering（AGE）は、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で提唱されている構造化されたエンジニアリング活動の 1 つである。[[DefinedTerm/briefing-engineering]] が作業を開始させるのに対し、AGE は、エージェントが生成した成果物や確認依頼を人間がどのようにレビューし応答するかを律し、人間の専門知識が最も大きな価値を生む箇所に的確に介入させる。

## 用法

同論文は AGE を人間のエンジニア（タスクの当初の起案者、またはドメインの専門家）に割り当てており、それは [[DefinedTerm/agent-command-environment]]（ACE）の中で行われる。同論文は ACE を、[[DefinedTerm/consultation-request-pack]]（CRP）の振り分け、[[DefinedTerm/merge-readiness-pack]]（MRP）の監査、構造化された裁定の発行のための、受信箱のようなインターフェースを提供するものとして説明している。AGE はこれら 2 種類のエージェント生成の成果物を入力とし、そのそれぞれに対して [[DefinedTerm/version-controlled-resolution]]（VCR）を生成する。VCR は対象とする成果物に明示的にリンクされ、トレーサビリティを保ち、後続の監査と学習を可能にする。

## 関連用語

[[DefinedTerm/consultation-request-pack]]、[[DefinedTerm/merge-readiness-pack]]、[[DefinedTerm/version-controlled-resolution]]
