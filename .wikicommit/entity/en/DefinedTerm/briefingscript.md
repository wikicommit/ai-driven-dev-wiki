---
title: "BriefingScript"
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
  description: "A structured, version-controlled, machine-readable artifact proposed in Structured Agentic Software Engineering (SASE) that serves as a detailed work order for an autonomous coding agent, combining success criteria, architectural context, strategic advice, and known pitfalls."
---

A BriefingScript is the artifact [[DefinedTerm/structured-agentic-software-engineering]] (SASE) proposes as the primary specification an "Agent Coach" gives an agent, introduced in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] as the product of [[DefinedTerm/briefing-engineering]]. It is described as more than a specification of intent: a detailed work order comparable to what a senior developer would give a junior one, unlike a traditional, implementation-agnostic Software Requirements Specification.

## Usage

A BriefingScript combines four kinds of content: **What & Success Criteria**, a verifiable checklist similar to Scrum's "Definition of Done" but enriched with formal, testable pre-conditions and invariants; **Architectural Context**, clarifying where the work fits in the system, including key modules, data models, or APIs; **Strategic Advice**, recommending specific implementation approaches such as libraries to use or patterns to avoid; and **Potential "Gotchas"**, highlighting known pitfalls such as subtle business logic, performance constraints, or dependency issues. The paper describes it as a living, version-controlled document evolving through iterative dialogue between the human coach and the agent rather than a rigid, one-shot, waterfall-style specification, and states it may be serialized in Markdown, YAML, JSON, or a domain-specific schema. It frames this as an agent-oriented evolution of Donald Knuth's "literate programming," shifting the primary artifact from code to the human-readable script that explains the logic and intent from which the agent's work is derived. A worked example implementing REST API rate limiting, structured into Goal & Why, What & Success Criteria, All Needed Context, Implementation Blueprint, and Validation Loop sections, is given in the paper's appendix.

## Related Terms

[[DefinedTerm/briefing-engineering]], [[DefinedTerm/product-requirement-prompt]], [[DefinedTerm/loopscript]], [[DefinedTerm/mentorscript]]
