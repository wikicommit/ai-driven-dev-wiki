---
title: "AgentScript"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-tooling, spec-driven-development, agent-architecture]
sources:
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/sdd/overview/'
    hash: sha256:946cf421ab8284921cee80b48fc236a89feb6dfd5c4a90f01ae072227495be73
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An approach in which the LLM emits a segment of plan code resembling JavaScript: the output is parsed into an abstract syntax tree and executed step by step by a runtime, which its source says makes the plan explicit, reviewable, pausable and serialisable."
  applicationCategory: "Agent planning"
  featureList: "LLM output as plan code resembling JavaScript; parsing into an abstract syntax tree; step-by-step execution by a runtime; explicit, reviewable, pausable and serialisable plans"
---

AgentScript is an approach to agent planning in which the model's plan is itself a program. Rather
than having the LLM describe what it intends to do and then act, it has the model emit a segment of
**plan code** resembling JavaScript; that output is parsed into an abstract syntax tree, and a
runtime executes it step by step.

The consequence its source draws is what the arrangement buys: the plan becomes explicit,
reviewable, pausable and serialisable, which it says raises the agent's interpretability and
controllability. The source lists it among the representative implementations of
[[DefinedTerm/spec-driven-development]], alongside AI IDEs, CLI toolkits and research frameworks, and
calls it a design for specification-driven agent *behaviour*.

## Capabilities

The one source held here describes the mechanism in outline only: LLM emits plan code → parse to AST
→ runtime executes stepwise. It does not describe the language's syntax, its tool-binding model, how a
paused plan is resumed, or who publishes it.

## Related Terms

- [[DefinedTerm/spec-driven-development]] — the practice the source lists this among the implementations of
- [[DefinedTerm/checkpoint-and-resume]] — a related idea; the source states that plans here are
  pausable and serialisable, but does not connect it to this term
- [[DefinedTerm/human-in-the-loop]] — a related idea; the source treats human confirmation at key
  steps under spec-driven development generally rather than in its account of this design
