---
title: "MentorScript"
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
  description: "A structured, version-controlled rulebook proposed in Structured Agentic Software Engineering (SASE) that codifies project norms and best-practice guidance for agents as 'mentorship-as-code,' replacing implicit, ephemeral code-review comments."
---

MentorScript is the artifact [[DefinedTerm/structured-agentic-software-engineering]] (SASE) proposes for codifying team norms and best practices for agents, introduced in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] as the product of [[DefinedTerm/ai-teammate-mentorship-engineering]] (ATME). The paper frames this as transforming mentorship from an implicit, ephemeral activity — comments in a code review — into an explicit, evolving, codified discipline it calls "mentorship-as-code."

## Usage

A MentorScript can hold rules ranging from granular checks (e.g. "all new functions must have deterministic tests") to high-level principles, and the paper states such rules should be subject to their own quality gates — linting, unit testing, and conflict detection — to keep them atomic and deterministic. Guidance can be explicit and durable (a direct, generalizable correction a human coach captures so the agent does not repeat a mistake) or inferred (an agent proposing a new general rule from a specific contextual correction, for the coach to approve). The paper states every action an agent takes should be traceable back to the MentorScript rules that were considered, using prompt-interpretation and reasoning-observability techniques, to enable rapid root-cause analysis when an agent's behavior deviates from expectations. It cites project-level configuration files such as CLAUDE.md, `.clinerules`, and AGENT.md — see [[DefinedTerm/agents-md]] — as an early, grassroots example of MentorScript-like artifacts, and notes the community currently has no consensus on what such files should contain or at what level of detail.

## Related Terms

[[DefinedTerm/ai-teammate-mentorship-engineering]], [[DefinedTerm/agents-md]], [[DefinedTerm/briefingscript]]
