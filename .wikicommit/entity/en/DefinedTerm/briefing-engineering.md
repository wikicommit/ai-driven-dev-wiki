---
title: "Briefing Engineering (BriefingEng)"
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
  description: "The engineering activity proposed in Structured Agentic Software Engineering (SASE) for authoring an agent's mission briefing — fusing requirements specification, architectural design, strategic implementation advice, and test planning into a single BriefingScript artifact."
---

Briefing Engineering (BriefingEng) is one of the structured engineering activities proposed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] as part of [[DefinedTerm/structured-agentic-software-engineering]] (SASE). The paper frames it as the activity through which an engineer's primary creative output shifts from implementation logic to the articulation of unambiguous intent and guidance, building on decades of work from the Requirements Engineering and Agile/Scrum communities rather than reinventing them. Its stated purpose is to move beyond the common failure pattern of pasting a raw, vague ticket and expecting an agent to produce good results, instead treating the mission brief as a first-class artifact.

## Usage

The paper assigns Briefing Engineering to the human Agent Coach, performed within the [[DefinedTerm/agent-command-environment]] (ACE), where AI assistance can help the coach author high-quality briefs by flagging ambiguity, surfacing edge cases, ensuring logical consistency, and generating property-based acceptance tests. Its artifact is the [[DefinedTerm/briefingscript]]. The paper's research roadmap for this activity calls for languages and schemas that express goals, constraints, invariants, domain context, and acceptance criteria without forcing premature design decisions; AI-powered authoring and review assistants that steer engineers toward property-based acceptance criteria rather than brittle examples; and traceability from generated code and evidence back to the briefing clauses that motivated them, which the paper says becomes especially important when a coach must compare and justify choices across multiple agent-generated alternatives (N-version programming).

## Related Terms

[[DefinedTerm/briefingscript]], [[DefinedTerm/structured-agentic-software-engineering]], [[DefinedTerm/product-requirement-prompt]]
