---
title: "cxdb"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-architecture, context-engineering]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Feb/7/software-factory/'
    hash: sha256:f037b61ef74329e98d22e3f5e86498585708d651d71581e420890095020b0ad3
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "StrongDM's AI context store: a system for holding agent conversation histories and tool outputs in an immutable DAG, released as a conventional multi-language codebase alongside their account of working without human code review."
  applicationCategory: "AI context store"
  author: "[[Organization/strongdm]]"
---

cxdb is [[Organization/strongdm]]'s AI context store — a system for storing conversation histories
and tool outputs in an immutable DAG. It was released publicly alongside the team's first account of
the [[DefinedTerm/software-factory]] arrangement they work under, and unlike the other release that
accompanied it, [[SoftwareApplication/attractor]], it is a conventional one: 16,000 lines of Rust, 9,500 of Go and 6,700 of
TypeScript.

## Capabilities
What is established about it is the shape of what it stores rather than its interface: the durable
record of an agent's work — the conversation history and the outputs of the tools it called — kept in
an immutable directed acyclic graph rather than overwritten in place. The post's author calls it similar to the SQLite
logging mechanism in his own LLM tool, but a whole lot more sophisticated — his impression rather
than a documented comparison.
That comparison is drawn in
[[BlogPosting/how-strongdms-ai-team-build-serious-software-without-even-looking-at-the-code]]. No
version is recorded.

## Adoption & Ecosystem
It was released by the same team that describes working without human code review, and what it
stores is conversation histories and tool outputs; the source states no role for it within that
arrangement, and none is assumed here. No adoption outside the team that built it is recorded.
Durable state for agent sessions is discussed more generally under
[[DefinedTerm/checkpoint-and-resume]] and [[DefinedTerm/context-engineering]].
