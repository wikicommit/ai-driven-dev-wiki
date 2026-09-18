---
title: "Agentic Guidance Engineering (AGE)"
type: "schema:DefinedTerm"
lang: en
tags: [sase]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "The engineering activity proposed in Structured Agentic Software Engineering (SASE) that governs the human's structured role in reviewing and responding to agent-generated Consultation Request Packs and Merge-Readiness Packs, elevating the human from a passive approver to an on-demand, targeted consultant."
---

Agentic Guidance Engineering (AGE) is one of the structured engineering activities proposed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] as part of [[DefinedTerm/structured-agentic-software-engineering]] (SASE). While [[DefinedTerm/briefing-engineering]] initiates work, AGE governs how a human reviews and responds to agent-generated artifacts and clarification requests, intervening precisely where their expertise adds the greatest value.

## Usage

The paper assigns AGE to the human engineer — either the task's original initiator or a domain specialist — performed within the [[DefinedTerm/agent-command-environment]] (ACE), which the paper describes as providing an inbox-like interface for triaging [[DefinedTerm/consultation-request-pack]]s (CRPs), auditing [[DefinedTerm/merge-readiness-pack]]s (MRPs), and issuing structured resolutions. AGE consumes these two agent-generated artifact types and produces a [[DefinedTerm/version-controlled-resolution]] (VCR) for each one, explicitly linked to the artifact it addresses to preserve traceability and enable downstream auditing and learning.

## Related Terms

[[DefinedTerm/consultation-request-pack]], [[DefinedTerm/merge-readiness-pack]], [[DefinedTerm/version-controlled-resolution]]
