---
title: "Plan-Do-Assess-Review (PDAR)"
type: "schema:DefinedTerm"
lang: en
tags: [spec-driven-development]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "An iterative task lifecycle — a human and AI plan, a dev-agent implements, the agent self-assesses, and a human reviews — formalized around Product Requirement Prompts, cited as a precursor to Structured Agentic Software Engineering's more team-level orchestration."
---

The Plan-Do-Assess-Review (PDAR) loop is an iterative workflow for a single agentic task's lifecycle, discussed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]]: a human and AI plan the work, a dev-agent implements it, an agent self-assesses the result, and a human reviews it. The paper describes it as commonly used together with a [[DefinedTerm/product-requirement-prompt]] (PRP), a "minimum viable packet" capturing goals, justification, acceptance criteria, and curated context, and cites Amazon's [[SoftwareApplication/kiro]] as an industry tool already demonstrating this spec-driven pattern.

## Usage

The paper credits PDAR as an early, crucial attempt to impose order on ad-hoc agentic prompting, and states its structured, testable intent aligns with [[DefinedTerm/structured-agentic-software-engineering]] (SASE)'s own insistence on structure. It positions PDAR as scoped to one-off task execution: by itself, it does not establish durable mentorship, agent lifecycle learning, or cross-task traceability, which SASE treats as first-class concerns addressed instead by artifacts such as [[DefinedTerm/mentorscript]] and [[DefinedTerm/loopscript]].

## When It Applies

The paper presents PDAR as an existing industry pattern — attributing the PRP structuring specifically to tools like Amazon's Kiro — rather than a practice it originates, and frames its own contribution as extending PDAR's single-task loop to team-level, N-to-N human-agent collaboration.

## Related Terms

[[DefinedTerm/product-requirement-prompt]], [[SoftwareApplication/kiro]], [[DefinedTerm/agentic-loop-engineering]]
