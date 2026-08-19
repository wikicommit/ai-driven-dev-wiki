---
title: "Subagent-Driven Development"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, agent-architecture, context-engineering]
sources:
  - type: url
    url: 'https://github.com/NeoLabHQ/context-engineering-kit'
    hash: sha256:bc2a9a7e51d46faa7b71b485a040ec8d6f6b10a78fc25f17a65dc7b9dde39b4c
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A development approach, named by the maintainers of Context Engineering Kit, in which a fresh subagent is dispatched for each task with a code review between tasks, so every unit of work starts from a clean context and passes a quality gate before the next begins."
  termCode: ""
  inDefinedTermSet: ""
---

Subagent-Driven Development (SADD) is an approach in which a fresh subagent is dispatched for each task, with a code review between tasks, so that every unit of work starts from a clean context window and clears a quality gate before the next one begins. The term is used by the maintainers of [[SoftwareApplication/context-engineering-kit]], who ship it as a plugin and describe its purpose as enabling fast iteration with quality gates.

## Usage

In the kit's implementation the approach is expressed as a set of commands rather than a single workflow: `/launch-sub-agent` for focused subagents with model selection and self-critique verification; `/do-and-judge` for a single task run by an implementation subagent, verified by an independent judge, with an automatic retry loop until it passes; `/do-in-parallel` for running the same task across multiple independent targets with context isolation; `/do-in-steps` for sequential orchestration with automatic decomposition and context passing between steps; and `/do-competitively` for competitive generation followed by multi-judge evaluation and evidence-based synthesis. A companion skill covers designing supervisor, peer-to-peer, and hierarchical architectures for tasks exceeding a single agent's context limits.

The maintainers position it as one point on a reliability-versus-cost curve rather than as the correct approach in all cases. In their own comparison table, `/do-and-judge` is credited with a 90% chance of a fully accurate result for changes spanning 1–3 files at 1.5×–3× token overhead, and `/do-in-steps` with 92% at 3×–5×, against 60–80% for a one-shot prompt at no overhead — with heavier spec-driven pipelines rated higher still at greater cost. These are the maintainers' own figures from their production usage, not published benchmark results.

They also describe SADD as a distilled version of their spec-driven development plugin, using meta-judge and judge sub-agents to generate specifications on the fly and in parallel with implementation, rather than writing a full specification up front.

## Related Terms

The approach is one way of applying [[DefinedTerm/subagents]] and overlaps with [[DefinedTerm/multi-agent-orchestration]]; its distinguishing feature is the per-task clean context plus an inter-task review gate, rather than parallel agents working simultaneously on one problem. Its review step is typically implemented as [[DefinedTerm/llm-as-judge]]. It contrasts with [[DefinedTerm/spec-driven-development]], which front-loads a written specification, and with [[DefinedTerm/ralph]], which achieves the same clean-context property through a loop that restarts rather than through dispatched subagents.
