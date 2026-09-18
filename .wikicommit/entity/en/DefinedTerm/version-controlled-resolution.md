---
title: "Version Controlled Resolution (VCR)"
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
  description: "An auditable artifact proposed in Structured Agentic Software Engineering (SASE) through which a human formally responds to and resolves a Consultation Request Pack or a Merge-Readiness Pack, explicitly linked to the artifact it addresses to preserve traceability."
---

A Version Controlled Resolution (VCR) is the artifact through which a human responds to an agent's [[DefinedTerm/consultation-request-pack]] (CRP) or [[DefinedTerm/merge-readiness-pack]] (MRP) in [[DefinedTerm/structured-agentic-software-engineering]] (SASE), introduced in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]]. Each Resolution is explicitly linked to the artifact it addresses, preserving traceability and enabling downstream auditing and learning, and is produced as the outcome of [[DefinedTerm/agentic-guidance-engineering]] (AGE) activities.

## Usage

The paper positions VCRs as the human side of a structured, version-controlled dialogue rather than an informal chat exchange: humans initiate work with a [[DefinedTerm/briefingscript]], [[DefinedTerm/loopscript]], and [[DefinedTerm/mentorscript]], agents respond with a CRP or MRP, and humans close the loop with a VCR — versioned updates to these artifacts capture clarification and feedback over time, keeping the shared understanding of tasks, processes, and team norms current.

## Related Terms

[[DefinedTerm/consultation-request-pack]], [[DefinedTerm/merge-readiness-pack]], [[DefinedTerm/agentic-guidance-engineering]]
