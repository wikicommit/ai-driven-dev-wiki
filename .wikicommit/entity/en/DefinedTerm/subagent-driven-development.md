---
title: "Subagent-driven development"
type: "schema:DefinedTerm"
lang: en
aliases: ["SADD"]
tags: [agents, context-window, llm, long-horizon-tasks]
sources:
  - type: url
    url: https://github.com/NeoLabHQ/context-engineering-kit
    hash: sha256:3a00d5fa6029f48343ba32101feda4acd0f31870b7ff74ef954be99d4e04a584
    license: GPL-3.0
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "Dispatching a freshly launched sub-agent for each task in a larger piece of work, with review between tasks, so that every step starts from a clean context under an orchestrating main agent."
---

Subagent-driven development is the practice of handing each task in a larger piece of work to a
freshly dispatched sub-agent, with code review between tasks, so that quality gates sit at every
step and no single agent accumulates the whole job in its context. A main agent acts as the
orchestrator: it launches the sub-agents, passes each what it needs, and controls their work. The
account here comes from one implementation, the Subagent-Driven Development plugin in
[[SoftwareApplication/context-engineering-kit]], which presents the approach as a distilled version
of [[DefinedTerm/spec-driven-development]] — generating specification material on the fly and in
parallel with implementation, through judge and meta-judge sub-agents, instead of producing a full
specification first.

## Usage
The reason given for launching a fresh sub-agent rather than continuing in one context is
[[DefinedTerm/context-rot]]: isolating independent agents keeps each one working on a short, clean
context, which the project argues holds the model near its best performance at every step. This is
the same reasoning behind a [[DefinedTerm/sub-agent-architecture]] generally, applied here to the
unit of work rather than to the shape of a system.

The implementation exposes the pattern as a set of execution primitives rather than a single
workflow: launching a focused sub-agent with self-critique verification, executing one task with an
independent judge and an automatic retry loop until it passes, running the same task across
independent targets in parallel with isolated contexts, decomposing a complex task into sequential
sub-agent steps that pass context forward, generating competing solutions and synthesising the best
one, exploring a solution space as a tree and pruning weak branches, and evaluating finished work
with one judge or several in debate. Alongside these it ships guidance on choosing between
supervisor, peer-to-peer and hierarchical multi-agent architectures for work that exceeds a single
agent's context limits.

## When It Applies
The approach applies where a job can be cut into steps that a sub-agent can complete from a
self-contained brief, and where the work is large enough that a single context would degrade before
the end. It assumes the orchestrator can decompose the task correctly and pass each sub-agent enough
context, since a sub-agent starting clean has only what it is given; a wrong decomposition is
therefore the failure that costs most, and the project's own advice to decompose deliberately
applies here as much as to the specification-driven route.

Its cost is duplicated context. The project's comparison places the judge-and-retry and
step-by-step variants between plain reflection and the full specification-driven route on both axes
— more reliable than a one-shot prompt, cheaper than a written specification, with token overhead a
small multiple of the baseline. Those figures are the project's own, drawn from its production use
rather than an independent benchmark.

How well established the approach is, this source cannot settle: it is one project's description of
its own tooling, resting on its own production use rather than on independent evaluation, and the
account above describes a single implementation.

## Related Terms
- [[DefinedTerm/sub-agent-architecture]] — the general arrangement this applies to units of work
- [[DefinedTerm/context-rot]] — the degradation it is designed to avoid
- [[DefinedTerm/spec-driven-development]] — the heavier approach it is presented as a distillation of
- [[DefinedTerm/llm-as-a-judge]] — the technique its judge sub-agents implement
