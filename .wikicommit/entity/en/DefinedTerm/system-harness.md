---
title: "System Harness"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, agent-tooling, orchestration, verification]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.17799'
    hash: sha256:98d0e3aebf3d1c5ab551f46a6c1f719389e820d2be1490bfefd669d87c107e69
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The outer orchestration layer around one or more language models that turns higher-level goals into concrete tasks, dispatches them to agent harnesses, manages the environment they act on, and routes their outputs through feedback — as distinguished from the agent harness, which is a single model working with tools towards a single task."
---

As set out in [[ScholarlyArticle/coding-benchmarks-are-misaligned-with-agentic-software-engineering]], a system harness is the outer orchestration layer around one or more large language models that manages tasks, environments and feedback over time. The paper distinguishes two levels of orchestration: the [[DefinedTerm/agent-harness]] is a language model interacting with tools, working towards a single task, with some system prompt and context to draw on, and most artefacts described as "coding agents" are agent harnesses in that sense; the system harness sits outside it and transforms higher-level goals into concrete tasks, dispatches each to one or more agent harnesses, manages the environment they act on, and routes their outputs through feedback that approximates whether the work is acceptable. The authors argue that practical agentic coding at scale operates at the level of the system harness, while current coding benchmarks operate at the level of the agent harness.

## Usage

The paper gives the system harness five recurring components. **Tasks** are units of work derived from higher-level goals. **Agent harnesses** are configurable executors composed of model, prompt, tools and loop, which the system harness may tune or treat as black boxes. The **environment** is the repository and runtime under change, together with integrated external services such as an issue tracker, CI and a deployment surface. **Context** is a curated projection of the environment and of harness-authored material — skills, plugins, hooks, specs — loaded into a particular invocation. **Feedback signals** are anything the harness reads to refine a solution or to refine itself, including tests, types, linters, formal verification, LLM-as-judge rubrics, pull-request comments, reviewer critique, production incidents and longer-horizon business signals; within feedback, *verifiers* are the strict subset that return a pass/fail verdict suitable for blocking.

Feedback is categorised into three tiers by scope, latency and trust. Inner-loop signals (seconds to minutes: tests, types, lint, compile) are fast and cheap but narrow, operating inside a single change attempt at commit or pull-request scope. Middle-loop signals (minutes to hours: reviewer requests, simulation, maintenance agents, score rubrics) aggregate over a wider slice of work and capture properties too broad or too judgement-dependent for a unit test — recurring review criticism, drift from project conventions, duplicated abstractions. Outer-loop signals (days to weeks: pull-request acceptance, revert rate, incident reports, customer feedback) are closest to ground truth but delayed and confounded. A second, orthogonal axis distinguishes signals the harness can modify, such as tests, from signals it cannot, such as human pull-request comments and business outcomes. The paper describes a productive system harness as using all three tiers: inner signals to refine a solution in-loop, middle signals to surface recurring issues and quality drift, and outer signals to calibrate which inner and middle proxies are worth trusting. All signals can take part in the harness's self-improvement loop, in which accumulated logs and recurring failures feed back into the harness's own components.

The authors note that many harnesses treat the issue tracker as the durable state machine for work and spawn per-task agent sessions. [[SoftwareApplication/ns2]], the harness they built and open-sourced, is the paper's worked example, and it cites Symphony and GasCity as other recent instances. Because the harness is a composition of components, the paper's central argument is that it is the harness — not the model alone — that should be the object of measurement, with components evaluated separately as well as in composition.

## Related Terms

- [[DefinedTerm/agent-harness]]
- [[DefinedTerm/agent-scaffold]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/agentic-loop-engineering]]
- [[DefinedTerm/harness-as-a-service]]
