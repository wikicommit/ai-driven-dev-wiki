---
title: "Execution Harness"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, agent-tooling, verification, agent-state, orchestration]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.20683'
    hash: sha256:4d2fd9336c3ac20f51ab2d6d4fc4eb98e0ba0673a8d3475e0e286c3fdfc4511a
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The runtime infrastructure surrounding a foundation model that realizes closed-loop agent execution, formalized by Guo et al. as six coupled responsibilities: observation interface, context manager, control loop, action interface, state and artifact store, and verification and governance."
---

The execution harness is the runtime infrastructure that surrounds a foundation model and realizes closed-loop agent execution. In [[ScholarlyArticle/survey-on-agent-system-and-harness-design]] an LLM-based agent is written as a model layer coupled with such a harness, and the harness is formalized as a six-part tuple — observation interface, context manager, control loop, action interface, state and artifact store, and verification and governance. The survey is explicit that this is broader than any individual tool, memory module, prompt template or workflow script: it is the coordinating layer that decides which observations reach the model, how context is assembled, how the agent loop advances, how actions are executed, how state and artifacts persist, and how failures are detected, governed and recovered. On this account the harness is not an optional engineering wrapper but the layer that turns model capability into sustained, inspectable interaction with an environment.

## Usage

The six responsibilities are described as follows. The **observation interface** converts raw environment signals — terminal output, file diffs, screenshots, web DOMs, API responses, event streams, logs — into observations the current model call can consume, with a dominant trade-off of richness versus tractability. The **context manager** determines what information enters the model context, when, and in what form, covering prompt construction, retrieval, memory selection, compression and summarization; its trade-off is fidelity versus manageability, and the survey argues the crucial distinction is not between long and short prompts but between monolithic and managed context. The **control loop** orchestrates the observe–reason–act–feedback cycle including step scheduling, stopping criteria, retries, reflection, delegation and handoffs, and in multi-model settings also model routing and role assignment; its trade-off is adaptability versus stability. The **action interface** maps model outputs to executable operations and defines tool granularity, specification, routing and permissions, trading flexibility against controllability. The **state and artifact store** persists execution state across steps, sessions and subtasks — plans, checkpoints, logs, traces, diffs, generated files, memory records — where the survey observes that long-horizon agents often fail not because no state is stored but because the wrong state is preserved, the right state cannot be retrieved, or stale state is treated as current. The **verification and governance layer** checks, constrains and repairs execution through tests, assertions, verifier models and judge signals, together with approval gates, sandboxing, budget control, rollback, retry, escalation and safe termination.

The decomposition is presented as operational rather than purely functional, and its components as coupled rather than independently optimizable: improving one layer can shift risk elsewhere, so that stronger compression can reduce cost while weakening downstream verification, richer actions can improve task coverage while increasing governance pressure, and more persistent state can improve continuity while introducing stale or conflicting evidence. The survey uses the same anatomy to read the task landscape, arguing that a task is a pressure profile over the six components rather than an application label — task horizon mostly stresses context, state and control; environment type mostly stresses observation, action and safety boundaries; and autonomy mostly stresses verification, logging and recovery.

Several infrastructure primitives are described as instantiating specific harness responsibilities rather than standing parallel to the harness: structured tool and function calling belongs primarily to the action interface while shaping context; the Model Context Protocol strengthens the boundary between context manager and action interface by reducing connector fragmentation; agent-to-agent communication protocols bear on the control loop and action interface; and sandboxed execution with approval policies belongs primarily to verification and governance. The survey also lists recurring design principles for harnesses — legibility, mechanical enforcement of safety-critical constraints rather than reliance on prompt obedience, verification in the loop, and explicit inspectable artifacts.

## Related Terms

- [[DefinedTerm/agent-harness]]
- [[DefinedTerm/system-harness]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/agent-scaffold]]
