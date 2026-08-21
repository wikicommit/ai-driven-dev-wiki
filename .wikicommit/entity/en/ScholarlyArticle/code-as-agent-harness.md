---
title: "Code as Agent Harness: Toward Executable, Verifiable, and Stateful Agent Systems"
type: "schema:ScholarlyArticle"
lang: en
tags: [agent-architecture, agentic-coding, context-engineering, multi-agent]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.18747'
    hash: sha256:b1035aaed7f12c5fa8504dac7f47c2e10dda381065834be2cea784c2f758fb1f
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A May 2026 survey from UIUC, Meta, and Stanford proposing 'code as agent harness' — the view that code has become an agent's operational substrate rather than only its output. It organises the field into three layers (harness interface, harness mechanisms, scaling to multi-agent) and names six open challenges for harness engineering."
  author:
    - "Xuying Ning"
    - "Katherine Tieu"
    - "Dongqi Fu"
    - "Tianxin Wei"
    - "Zihao Li"
    - "Yuanchen Bei"
  datePublished: "2026-05-18"
  keywords:
    - "[[DefinedTerm/agent-harness]]"
    - "[[DefinedTerm/harness-engineering]]"
    - "[[DefinedTerm/agentic-coding]]"
---

"Code as Agent Harness" is a large survey posted to arXiv on 18 May 2026 by a group spanning the University of Illinois Urbana-Champaign, Meta, and Stanford University, with a long author list, six of whose members are marked as core contributors. It lists its own keywords as agent harness, coding agent, harness engineering, and agentic AI, and maintains an accompanying paper list.

Its organising claim is a change of role rather than of capability: "In emerging agentic systems, code is no longer only a target output. It increasingly serves as an operational substrate for agent reasoning, acting, environment modeling, and execution-based verification." The survey frames that shift through [[DefinedTerm/agent-harness]] and introduces **code as agent harness** as "a unified view that centers code as the basis for agent infrastructure."

## Key Contributions

The survey is organised around three connected layers.

- **The harness interface** — where code connects agents to reasoning, action, and environment modeling. Under reasoning it covers program-delegated reasoning, formal verification and symbolic reasoning interfaces, and iterative code-grounded reasoning; under acting, grounded skill selection, programmatic policy generation, and lifelong code-based agents; under environment, structured world representations, execution-trace world modeling, code-grounded evaluation environments, and verifiable environment construction.
- **Harness mechanisms** — planning, memory, and tool use for long-horizon execution, "together with feedback-driven control and optimization that make harness reliable and adaptive." Its planning taxonomy is linear decomposition, structure-grounded, search-based, and orchestration-based; its memory taxonomy separates working, semantic, experiential, long-term, and multi-agent memory alongside context compaction and state offloading; its tool-use taxonomy is function-oriented, environment-interaction, verification-driven, and workflow-orchestration. Control is organised as a plan–execute–verify loop covering harness-level control, planning as contract formation, sandboxed execution with permissioned state transition, and verification through deterministic sensors.
- **Scaling the harness** — from single-agent systems to multi-agent settings, "where shared code artifacts support multi-agent coordination, review, and verification." This part covers functional role specialization and human-guided planning, interaction modes grounded in shared program state, workflow topology, execution-feedback integration and shared-harness synchronization, and closes with a position section arguing for a shared code-centric harness substrate.

Across those layers it summarises methods and applications spanning coding assistants, GUI and OS automation, embodied agents, scientific discovery, personalization and recommendation, DevOps, and enterprise workflows.

## Notes

The survey names six open challenges for harness engineering: evaluation beyond final task success; verification under incomplete feedback; regression-free harness improvement; consistent shared state across multiple agents; human oversight for safety-critical actions; and extensions to multimodal environments.

Two of those connect directly to material already recorded here. "Regression-free harness improvement" is the problem [[ScholarlyArticle/dont-blame-the-large-language-model]] measures empirically — that successive harness releases do not reliably improve, and sometimes degrade, agent quality — and "evaluation beyond final task success" is the same gap that study fills by measuring token consumption and tool-call overhead alongside resolve rate. The survey also contains a section on adaptive harness optimization built around deep telemetry, an evolution agent, and governed harness mutation, which is the automated form of what [[DefinedTerm/harness-engineering]] describes as a manual practice.

This is a survey of the literature rather than new measurement: it contributes a taxonomy and a framing, and the claims within it belong to the works it reviews rather than to the authors. The material summarised on this page comes from its abstract, introduction, and section structure.
