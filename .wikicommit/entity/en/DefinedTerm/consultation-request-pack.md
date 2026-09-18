---
title: "Consultation Request Pack (CRP)"
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
  description: "A structured artifact proposed in Structured Agentic Software Engineering (SASE) that an agent generates to formally escalate a decision or uncertainty to a human specialist, turning ad-hoc human consultation into a traceable team artifact."
---

A Consultation Request Pack (CRP) is the artifact an agent generates in [[DefinedTerm/structured-agentic-software-engineering]] (SASE), introduced in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]], when it requires human input to proceed. It is contextualized by the active [[DefinedTerm/briefingscript]] and may be triggered by [[DefinedTerm/loopscript]] or [[DefinedTerm/mentorscript]] rules; it documents the specific uncertainty or decision point the agent has encountered.

## Usage

The [[DefinedTerm/agent-command-environment]] (ACE) routes, presents, and records each CRP, treating the targeted human as a callable expertise endpoint while preserving the context needed for accountability. The paper's worked appendix example shows an agent escalating a conflict between a BriefingScript's specified Redis backend and a known "gotcha" about replication lag for a high-stakes payment endpoint, presenting the human decider with structured options (each with pros, cons, and estimated effort), the agent's own recommendation and reasoning, and an escalation target (e.g. "Tech Lead or Architect role"). A human responds to a CRP with a [[DefinedTerm/version-controlled-resolution]] (VCR), which is explicitly linked back to the CRP it addresses to preserve traceability for downstream auditing and learning.

## Related Terms

[[DefinedTerm/version-controlled-resolution]], [[DefinedTerm/agentic-guidance-engineering]], [[DefinedTerm/merge-readiness-pack]]
