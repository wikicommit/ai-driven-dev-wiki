---
title: "Code as Agent Harness: Toward Executable, Verifiable, and Stateful Agent Systems"
type: "schema:ScholarlyArticle"
lang: en
tags: [agent-harness, survey, agent-architecture, multi-agent-systems, verification]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.18747'
    hash: sha256:b1035aaed7f12c5fa8504dac7f47c2e10dda381065834be2cea784c2f758fb1f
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A survey framing code as the operational substrate — the harness — of agentic AI systems, organised into the harness interface, harness mechanisms, and multi-agent scaling over shared code."
  author: ["Xuying Ning", "Katherine Tieu", "Dongqi Fu", "Tianxin Wei", "Zihao Li", "Yuanchen Bei"]
  datePublished: "2026"
  keywords: ["agent harness", "coding agent", "harness engineering", "agentic AI"]
---

A large survey, authored by a group of more than forty researchers spanning the University of Illinois Urbana-Champaign, Meta and Stanford University, arguing that code in agentic systems has stopped being only a target output and become an operational substrate for reasoning, acting, environment modelling and execution-based verification. The six names recorded above are those the paper marks as core contributors. The authors frame this shift through the lens of the agent harness and introduce "code as agent harness" as a unified view.

Their argument for why code specifically is that it has three properties that make it work as a harness interface rather than merely as a notation: it is **executable**, so model outputs become operations with formally verifiable outcomes; **inspectable**, so intermediate computation is exposed as structured traces the harness can read, store and act on; and **stateful**, so the evolving program represents task progress in a persistent, modifiable form across steps. The paper is careful to bound what it means by code — executable or machine-checkable artefacts including programs, scripts, formal specifications, proof scripts, API schemas, tool definitions, tests, repositories, simulators and configuration files — and to say that raw perception, physical state, human intent and model-internal reasoning are not themselves code, even where they can be sensed, serialised or acted upon through it.

The survey is organised into three connected layers: the harness interface, where code connects agents to reasoning, action and environment modelling; harness mechanisms, covering planning, memory, tool use, feedback-driven control and optimisation; and the scaling of the harness from single-agent to multi-agent settings, where shared code artefacts support coordination, review and verification.

## Key Points

- The authors organise the harness interface into three roles code plays: code for reasoning, which externalises internal logic into verifiable computation; code for acting, which translates high-level intent into executable operations grounded in embodied, GUI, software or tool-use environments; and code for environment modelling, which represents world state and transition dynamics through program states, repositories, simulators, tests and logs.
- They frame harness control as a **Plan–Execute–Verify loop**, in which plans form contracts over intended changes, execution applies them inside sandboxed and permissioned environments, and verification uses deterministic sensors and human-review gates to decide whether state should be accepted, revised, escalated or rolled back.
- Memory is characterised not as a larger context window or a vector database but as a state-management layer, decomposed into working, semantic, experiential, long-term and multi-agent memory, with context compaction and state offloading as cross-cutting mechanisms controlling the boundary between active context and durable task state.
- They propose a multi-tier permission model separating low-risk observation from high-risk action — a read-only tier, a sandbox-edit tier, and a full-access tier covering network access, credentials, deployment and destructive operations — and argue actions in the final tier should be guarded by mandatory human-in-the-loop gates.
- **Agentic Harness Engineering** is named as a distinct discipline: treating the operating environment itself as the object of analysis, driven by deep telemetry and acted on by an Evolution Agent that revises harness components under governed mutation.
- The survey's stated central gap in the multi-agent literature is that the majority of surveyed systems represent shared state only implicitly, as the current code file plus conversational history, with no persistent queryable representation — so an agent's belief about the code state can diverge from the true state undetectably.
- The authors identify two related patterns as consequences of that gap: topology complexity correlates inversely with harness-state formality, with implicit-state systems developing elaborate adaptive topologies as a structural workaround; and sophisticated context-management mechanisms are described as "the tax of implicit shared state".
- They report a finding that complicates the case for execution grounding: surveyed systems demonstrate that LLM-simulated execution can achieve over 98% precision and recall in predicting actual outcomes without running code, suggesting execution feedback's value is not uniform across failure modes, and proposing a mature harness would use linguistic reasoning as a fast path and delegate to execution only for failure modes that require it.
- Seven open problems are set out: harness-level evaluation and oracle adequacy, semantic verification beyond executable feedback, self-evolving harnesses without regression, transactional shared program state and semantic conflict resolution, human-in-the-loop safety and accountability as harness state, multimodal code-harness systems, and a science of harness engineering.
- The survey's closing position is that the most important future systems will combine four properties — executable, inspectable, stateful and governed.

## Notes

On evaluation, the authors argue that once an LLM is embedded in a harness, end-task success metrics conflate the base model's capability, the harness's quality, tool reliability, feedback informativeness and environment difficulty. They propose complementing final task accuracy with harness-level metrics covering trajectory efficiency, verification strength, recovery ability, state consistency, safety compliance and replayability, and name oracle adequacy — whether the evaluator captures the intended task rather than a narrow executable proxy — as the central bottleneck.

A related caution runs through the verification discussion: because execution feedback is available, a harness can become overconfident precisely because it has it. The authors' proposed response is a verification stack with explicit scope, composing multiple artefacts — unit tests, property-based tests, fuzzers, static analysers, type checkers, security scanners, runtime monitors, formal specifications, human review — where each declares what it verifies, what it cannot verify, and what confidence it provides, with every accepted action carrying an evidence bundle.

The survey also observes that production harnesses are becoming a source of training data for the next generation of code-assistant models, which it describes as making the boundary between "the agent" and "the harness around the agent" a learnable surface in its own right.

A companion paper list is published at <https://github.com/YennNing/Awesome-Code-as-Agent-Harness-Papers> .
