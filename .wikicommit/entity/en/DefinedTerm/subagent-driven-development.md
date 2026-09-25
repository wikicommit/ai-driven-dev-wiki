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
  - type: url
    url: 'https://github.com/obra/superpowers'
    hash: sha256:61b63ad03aa78e57f0017d8bda85982ec6437837fe3cdff96e12cd23ffb45b76
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Dispatching a freshly launched sub-agent for each task in a larger piece of work, with review between tasks, so that every step starts from a clean context under an orchestrating main agent."
---

Subagent-driven development is the practice of handing each task in a larger piece of work to a
freshly dispatched sub-agent, with code review between tasks, so that quality gates sit at every
step and no single agent accumulates the whole job in its context. A main agent acts as the
orchestrator: it launches the sub-agents, passes each what it needs, and controls their work. Two
implementations are described here, and they place the practice differently. The Subagent-Driven
Development plugin in [[SoftwareApplication/context-engineering-kit]] presents it as a distilled
version of [[DefinedTerm/spec-driven-development]] — generating specification material on the fly
and in parallel with implementation, through judge and meta-judge sub-agents, instead of producing a
full specification first. [[SoftwareApplication/superpowers]] instead places it after a design has
been agreed and written up as a detailed plan, as the step that executes that plan.

## Usage
The reason given for launching a fresh sub-agent rather than continuing in one context is
[[DefinedTerm/context-rot]]: isolating independent agents keeps each one working on a short, clean
context, which the project argues holds the model near its best performance at every step. This is
the same reasoning behind a [[DefinedTerm/sub-agent-architecture]] generally, applied here to the
unit of work rather than to the shape of a system.

The Context Engineering Kit exposes the pattern as a set of execution primitives rather than a single
workflow: launching a focused sub-agent with self-critique verification, executing one task with an
independent judge and an automatic retry loop until it passes, running the same task across
independent targets in parallel with isolated contexts, decomposing a complex task into sequential
sub-agent steps that pass context forward, generating competing solutions and synthesising the best
one, exploring a solution space as a tree and pruning weak branches, and evaluating finished work
with one judge or several in debate. Alongside these it ships guidance on choosing between
supervisor, peer-to-peer and hierarchical multi-agent architectures for work that exceeds a single
agent's context limits.

In Superpowers the practice is one skill in a numbered sequence of workflow skills. It activates once a plan exists — a
plan broken into tasks of two to five minutes, each with exact file paths, complete code and
verification steps — and dispatches a fresh subagent per task with a review after each; the skill
library describes that review as two-stage, checking spec compliance first and code quality second.
The same point in the sequence offers an alternative, executing the plan inline in the current
session with a single fresh review of the whole branch at the end, and the project frames the choice
as a trade-off: subagent-driven development as the most thorough option, inline execution as the
cheapest. Its README says it is not uncommon for an agent working this way to run autonomously for a
couple of hours without deviating from the plan.

## When It Applies
The approach applies where a job can be cut into steps that a sub-agent can complete from a
self-contained brief, and where the work is large enough that a single context would degrade before
the end. It assumes the orchestrator can decompose the task correctly and pass each sub-agent enough
context, since a sub-agent starting clean has only what it is given. The Context Engineering Kit's
guidance for its specification-driven plugin reports that an agent starting from an incorrect
specification can still self-correct but takes much longer and spends time on wrong paths, and
strongly advises decomposing work into smaller tasks with dependencies. In Superpowers the per-task
subagents only start after the design has been approved and the plan written down.

Its cost is token overhead. The Context Engineering Kit's comparison places the judge-and-retry and
step-by-step variants broadly between plain reflection and the full specification-driven route —
generally more reliable than a one-shot prompt and cheaper than a written specification, with a
reported token overhead of 1.5x-3x and 3x-5x respectively. Those figures are the project's own, drawn from its production use
rather than an independent benchmark.

How well established the approach is, these sources cannot settle: each is a project's description of
its own tooling, resting on its own use rather than on independent evaluation. Two toolkits ship a
practice under this name, and the sources do not say whether one derives from the other.

## Related Terms
- [[DefinedTerm/sub-agent-architecture]] — the general arrangement this applies to units of work
- [[DefinedTerm/context-rot]] — the degradation it is designed to avoid
- [[DefinedTerm/spec-driven-development]] — the heavier approach it is presented as a distillation of
- [[DefinedTerm/llm-as-a-judge]] — the technique the Context Engineering Kit's judge sub-agents implement
- [[SoftwareApplication/superpowers]] — a skills plugin that ships the practice as one step of its workflow
