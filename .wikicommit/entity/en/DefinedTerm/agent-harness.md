---
title: "Agent Harness"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, agent-tooling, verification, agent-state]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.18747'
    hash: sha256:b1035aaed7f12c5fa8504dac7f47c2e10dda381065834be2cea784c2f758fb1f
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The policy-governed system around a language model that grounds its outputs in external execution, persistent state and verifiable feedback, turning a stateless model into a functional agent."
---

An agent harness is what turns a stateless language model into a functional agent, by grounding its outputs in external execution, persistent state and verifiable feedback. [[ScholarlyArticle/code-as-agent-harness]] frames the central design question for any harness as a question about medium — what connects the model to its task environment — and argues that code is the answer, because code is executable, inspectable and stateful in ways natural language is not. On that account these are not properties of code as a notation but the properties that make it function as a harness interface: executability means the harness can verify what the model intended, inspectability means failures can be diagnosed and fed back, and statefulness means the agent's interaction history is not lost between steps.

## Usage

The survey distinguishes the harness from the code running inside it. Code is an executable medium *within* the harness; the harness is the larger policy-governed system deciding what code may be executed, trusted, persisted, reused or promoted into future workflows. Reliability, on this framing, depends not only on the model's judgement and on agent-authored artefacts but on human-designed policies, sandbox boundaries, permission tiers, verification oracles, audit logs and human-review gates.

Three roles are identified for code at the harness interface. **Code for reasoning** externalises internal logic into verifiable computation that interpreters, symbolic solvers or execution traces can check and refine. **Code for acting** translates high-level intent into executable operations grounded in embodied, GUI, software or tool-use environments — with the survey emphasising that executable action code is an interface to perception, affordance estimation, controllers and safety layers, not a replacement for them. **Code for environment modelling** represents world state, transition dynamics and feedback signals through program states, repositories, simulators, tests and logs the agent can execute, edit and query.

Above that interface sit the harness mechanisms the survey groups into five interacting categories: planning, which organises long-horizon execution; memory and context engineering, described as a state-management layer deciding what stays in active context, what is compacted into summaries and what is offloaded to durable external storage; tool use, treated as a governed interface between model intent and external systems rather than an auxiliary capability; control through the [[DefinedTerm/plan-execute-verify-loop]]; and [[DefinedTerm/harness-engineering]], which studies how the harness itself can be measured and improved.

The survey also treats the harness as a safety governor rather than only a context manager or tool executor — a layer that classifies proposed actions by risk, enforces permission tiers, denies actions violating hard constraints and requires human approval for irreversible or externally consequential transitions. Its proposed structure is a multi-tier permission model: a read-only tier for browsing, retrieval, static inspection and log analysis; a sandbox-edit tier for local patching, test execution and temporary dependency installation inside an isolated workspace; and a full-access tier covering network access, credentials, deployment commands, package publishing, destructive filesystem operations and Git history mutation. The authors argue permissions should depend not only on tool identity but also on arguments, environment state, data sensitivity and expected side effects, since the same command may be safe in a disposable sandbox and unsafe in a production repository.

A further argument the survey makes about safety is that human-in-the-loop control should become durable harness state rather than an occasional prompt interruption: each approval, rejection, policy exception or reviewer correction should update the harness's permission rules, escalation policy, verification criteria and future memory retrieval, and high-stakes approvals should be auditable state transitions recording what was proposed, what evidence was shown, what risks were surfaced, who decided and what responsibility boundary changed. The authors call this executable accountability.

## Related Terms

- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/plan-execute-verify-loop]]
- [[DefinedTerm/agent-scaffold]]
- [[DefinedTerm/harness-as-a-service]]
- [[DefinedTerm/ai-coding-agent]]
