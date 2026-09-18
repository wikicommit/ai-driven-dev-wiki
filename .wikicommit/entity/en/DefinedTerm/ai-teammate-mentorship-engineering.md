---
title: "AI Teammate Mentorship Engineering (ATME)"
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
  description: "The engineering activity proposed in Structured Agentic Software Engineering (SASE) for codifying project norms and best practices for agents as 'mentorship-as-code' via a version-controlled MentorScript, so guidance is durable and auditable rather than implicit and ephemeral."
---

AI Teammate Mentorship Engineering (ATME) is one of the structured engineering activities proposed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] as part of [[DefinedTerm/structured-agentic-software-engineering]] (SASE). Its stated purpose is to ensure agent-generated code is not just functional but maintainable and aligned with team culture, by treating agent guidance as first-class code — what the paper calls "mentorship-as-code."

## Usage

The paper assigns guidance under ATME to the human coach, durably consumed by agents; rules are authored in the [[DefinedTerm/agent-command-environment]] (ACE) and directly influence agent behavior in the [[DefinedTerm/agent-execution-environment]] (AEE). Its artifact is the [[DefinedTerm/mentorscript]]. The paper's research roadmap for this activity calls for abstractions expressive enough for nuanced guidance but simple enough for teams to review as ordinary engineering artifacts; quality assurance for mentorship rules themselves — linting, testing, conflict detection, and regression checks, studying how to verify new rules improve agent behavior without unintended side effects elsewhere; and mechanisms for agents to learn and explain candidate rules from repeated human feedback while keeping those rules reviewable and auditable, connecting an agent's decision to the specific rules it considered.

## Related Terms

[[DefinedTerm/mentorscript]], [[DefinedTerm/agents-md]], [[DefinedTerm/structured-agentic-software-engineering]]
