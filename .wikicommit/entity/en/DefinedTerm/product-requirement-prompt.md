---
title: "Product Requirement Prompt (PRP)"
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
  description: "A 'minimum viable packet' specification pattern for an agentic coding task, structured into five sections — Goal & Why, What & Success Criteria, All Needed Context, Implementation Blueprint, and Validation Loop — demonstrated by industry tools such as Amazon's Kiro."
---

A Product Requirement Prompt (PRP) is a specification artifact discussed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] that captures a task's goals, justification, acceptance criteria, and curated context as a "minimum viable packet" for an AI coding agent. The paper describes industry tools such as Amazon's [[SoftwareApplication/kiro]] as already demonstrating this spec-driven development pattern.

## Usage

The paper describes a PRP as typically structured into five sections: (1) Goal & Why, setting the objective and business value; (2) What & Success Criteria, defining scope with verifiable conditions and invariants; (3) All Needed Context, curating relevant documentation and known pitfalls without overloading the agent's context; (4) Implementation Blueprint, providing strategic guidance and constraints rather than a low-level plan; and (5) Validation Loop, codifying the acceptance-testing strategy. It is used within a [[DefinedTerm/plan-do-assess-review]] (PDAR) loop, and the paper aligns PRPs with SASE's own [[DefinedTerm/briefingscript]], noting both insist on structured, testable intent.

## Related Terms

[[DefinedTerm/plan-do-assess-review]], [[SoftwareApplication/kiro]], [[DefinedTerm/briefingscript]]
