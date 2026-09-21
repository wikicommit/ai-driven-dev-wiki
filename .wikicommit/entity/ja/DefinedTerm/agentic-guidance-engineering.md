---
title: "Agentic Guidance Engineering（AGE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agentic-guidance-engineering.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）が提唱するエンジニアリング活動の 1 つ。エージェントが生成した Consultation Request Pack と Merge-Readiness Pack をレビューし、それに応答するという人間の構造化された役割を規定するもので、人間を受動的な承認者から、必要に応じて的を絞って助言するコンサルタントへと引き上げる。"
---

Agentic Guidance Engineering（AGE）は、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] が [[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として提唱する、構造化されたエンジニアリング活動の 1 つである。[[DefinedTerm/briefing-engineering]] が作業を起動するのに対し、AGE は、人間がエージェント生成の成果物や確認依頼をどうレビューし、どう応答するかを規定し、自らの専門性が最も価値を生む箇所に的を絞って介入させる。

## 用法

論文は AGE を人間のエンジニア — そのタスクを最初に立ち上げた本人か、あるいは領域の専門家 — に割り当て、[[DefinedTerm/agent-command-environment]]（ACE）の中で行われるものとしている。論文は ACE を、[[DefinedTerm/consultation-request-pack]]（CRP）の仕分け、[[DefinedTerm/merge-readiness-pack]]（MRP）の監査、そして構造化された裁定の発行を行うための、受信箱のようなインターフェースを提供するものとして説明している。AGE はこの 2 種類のエージェント生成成果物を入力として受け取り、それぞれに対して [[DefinedTerm/version-controlled-resolution]]（VCR）を生成する。VCR は対象となる成果物に明示的に紐付けられ、追跡可能性を保ち、後続の監査と学習を可能にする。

## 関連用語

[[DefinedTerm/consultation-request-pack]]、[[DefinedTerm/merge-readiness-pack]]、[[DefinedTerm/version-controlled-resolution]]
