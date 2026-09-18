---
title: "Agentic Agile-V"
type: "schema:DefinedTerm"
lang: en
tags: [agents, verification, software-process]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.20456'
    hash: sha256:fcf0fa7c744985d64d3d71a71e82e882a7ad1f5133fca691f23cb211cd7ae8b3
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A two-layer process framework for agentic software, firmware and hardware development, proposed by Koch, pairing an Agile-V lifecycle backbone with a task-level SCOPE-V loop so that agent-generated work is accepted on evidence proportionate to its risk rather than on plausibility."
---

Agentic Agile-V is a process framework for agentic software, firmware and hardware development, proposed by Koch in [[ScholarlyArticle/agentic-agile-v]]. It has two layers. The macro layer is Agile-V, an iterative lifecycle in which each increment remains traceable through requirements, design, implementation, verification, approval and audit evidence. The micro layer is SCOPE-V, a six-step loop run for each individual agentic task. The author states the division as Agile-V controlling the lifecycle and SCOPE-V controlling the agentic task, and presents the pairing as a way to avoid choosing between agility and verification: Agile iteration supplies speed, V-model reasoning supplies traceability, agentic execution supplies implementation capacity, and verification gates decide acceptance.

## Usage

The SCOPE-V loop's six steps are Specify, Constrain, Orchestrate, Prove, Evolve and Verify. Specify converts intent into a task brief carrying objective, scope, non-goals, affected modules, dependencies, acceptance criteria and required evidence. Constrain sets boundaries — no public API change without approval, no unrelated files, no new dependencies without justification, no broad refactor during a bug fix, explicit review for security-sensitive code, and preservation of hardware timing and safety constraints. Orchestrate defines how the agent should work: inspect first, summarize the current design, propose a plan, implement small slices, run local checks and produce a diff summary with residual risks. Prove requires evidence proportionate to risk, from unit tests and static analysis through to simulation, formal checks and hardware-in-the-loop results. Evolve feeds validated learning back into repository instructions, templates, tests and baselines while removing stale or harmful instructions. Verify is treated as recurring rather than final — before implementation, during patching, before merge, after deployment and after field feedback.

Ahead of the loop sits what the author calls a conversation-to-contract gate. Conversation is held to be appropriate for early uncertainty — clarifying requirements, brainstorming architecture, identifying missing constraints, comparing test strategies and exploring alternatives — with the agent acting as a thinking partner whose desired output is a better problem statement rather than code. Structure becomes mandatory once a task affects public APIs, safety, security, performance, hardware behaviour, regulated workflows, customer-facing behaviour, shared libraries or persistent data. The rule the author states is not to let an agent implement from a long chat, but from a reviewed brief.

Acceptance is governed by four risk levels with escalating requirements, from exploratory work needing only a smoke test and optional review, through routine and production tiers, to high-assurance work requiring traceable requirements, independent tests, simulation or formal or hardware-in-the-loop evidence where applicable, and explicit sign-off. For the upper two tiers the framework specifies a minimum evidence bundle: task brief and requirement identifiers, the agent's plan and affected files, executed commands and test results, a diff summary with residual risks, a trace from acceptance criteria to tests, the reviewer's decision, and a rollback path.

## When It Applies

The framework assumes agents capable of inspecting repositories, planning, editing files, running tests and producing diffs, and a team willing to supply structured input rather than conversational prompts — the author sets out a minimum input-artifact package covering intent and scope, acceptance criteria, architecture context, constraints, execution context, evidence requirements and a risk class, with a parallel column of hardware equivalents such as board revision, memory map, clocks, pinout and toolchain. It is aimed squarely at the failure mode it calls [[DefinedTerm/verification-debt]], and its risk tiers exist so that the overhead is not applied uniformly: exploratory work is meant to stay light.

Its stated boundary is the same one the author draws around his evidence. The framework is a synthesis and process proposal rather than a validated intervention: he calls for it to be evaluated empirically across multiple teams, repositories, tools and hardware domains, and lists as open questions whether structured execution briefs actually improve agent success over conversational prompts, which task classes benefit rather than being slowed by the overhead, and whether evidence bundles can reduce verification debt without eliminating productivity gains. The minimal-context principle it adopts for repository instructions — short, current, non-contradictory, tied to executable feedback — is likewise derived from conflicting studies rather than from a measurement of the framework itself.

## Related Terms

[[ScholarlyArticle/agentic-agile-v]], [[DefinedTerm/verification-debt]], [[DefinedTerm/vibe-coding]], [[DefinedTerm/spec-driven-development]], [[DefinedTerm/agents-md]]
