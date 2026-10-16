---
title: "Executable attention"
type: "schema:DefinedTerm"
lang: en
tags: [harness-engineering, coding-agents, verification]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/are-harnesses-worth-the-cost.html'
    hash: sha256:3baedf6f6c5150f062e0a3c5f7a5c6d8a88fe3edce290137be55d057888a85dc
review_status: pending
generated_at: "2026-10-16"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.10.0"

properties:
  description: "A way of describing what a behavioral harness does for a coding agent: by turning written requirements into executable feedback, it brings requirements the agent dropped during implementation back into focus when a sensor goes red."
---

Executable attention is a term Naresh Jain uses in
[[BlogPosting/are-harnesses-worth-the-cost]] for the effect of a behavioral harness on a coding agent:
the harness turns written requirements into environmental feedback, so that when a sensor goes red a
requirement the agent was given but did not fully implement is brought back into focus and the agent
gets another opportunity to act on it. The term pairs with what the author calls an *attention lapse*
— code that omits or incompletely implements a requirement that was explicit in the agent's
instructions. In his interpretation the harness serves as an external memory and attention aid.

## Usage

The term comes from an experiment in which coding agents built the same API service with and without a
behavioral harness of [[DefinedTerm/guides-and-sensors]]. A cost-optimized model's unharnessed runs
missed details that the brief clearly specified — a deferred-creation timeout workflow, a Kafka wire
contract, exact error responses — while the harnessed runs all passed the external evaluation. The
author offers executable attention as his reading of why, and says that the experiment did not
establish the cause of the lapses; he suggests that juggling library choices, boilerplate, dependency
injection and asynchronous wiring across a growing context may contribute.

## When It Applies

As the author frames it, executable attention is what sensors provide when they run *during*
development, and it matters for models whose unaided attempts produce inconsistent outcomes. For
frontier models that solve the task in one pass, he recommends running the same sensors once as a final
verification gate instead, because running them continuously added overhead without a detected benefit.
It assumes the checks encode the right expectations: they can enforce only what humans have written
into the contracts and examples, which need reviewing and maintaining alongside the implementation.
The idea rests on a single experiment — 10 runs per model on one greenfield Java service with an
unusually detailed brief — and is presented as the author's interpretation and a conditional
hypothesis, not an established result.

## Related Terms

- [[DefinedTerm/guides-and-sensors]]
- [[DefinedTerm/harness-engineering]]
