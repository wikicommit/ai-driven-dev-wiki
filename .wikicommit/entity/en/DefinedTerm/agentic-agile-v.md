---
title: "Agentic Agile-V"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, software-development-process, verification, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.20456'
    hash: sha256:fcf0fa7c744985d64d3d71a71e82e882a7ad1f5133fca691f23cb211cd7ae8b3
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A two-layer process framework proposed by Koch for agentic software, firmware, and hardware development: an Agile-V lifecycle backbone providing iteration with V-model traceability, and a task-level SCOPE-V loop that converts conversational intent into structured artifacts and acceptance evidence."
---

Agentic Agile-V is a process framework proposed by Christopher Koch in [[ScholarlyArticle/agentic-agile-v]] for agentic software, firmware, and hardware development. It has two layers: a macro layer, Agile-V, an iterative lifecycle in which each increment remains traceable to requirements, design, implementation, verification, approval, and audit evidence; and a micro layer, the [[DefinedTerm/scope-v]] loop, used to run individual agentic tasks. The design principle is stated as a division of responsibility — Agile-V controls the lifecycle; SCOPE-V controls the agentic task.

## Usage

The framework is motivated by a diagnosed gap rather than by a claim about model capability. Koch argues that current tools provide execution surfaces, sandboxing, repository instructions, test execution, and pull-request workflows, while existing engineering processes provide requirements discipline, verification logic, review, and release gates — and that what is missing is a lightweight framework telling teams what input to provide to agents, how to structure agent execution, when to test, and which evidence is required before accepting generated artifacts.

Its organizing principle is a three-part statement: conversation is useful for discovering intent; structured artifacts are required for implementation; evidence is required for acceptance. The paper argues this design avoids a false choice between agility and verification, since Agile iteration provides speed, V-model reasoning provides traceability, agentic execution provides implementation capacity, and verification gates decide acceptance.

Three mechanisms operationalize it.

**A conversation-to-contract gate.** Koch argues long chat histories are not reliable engineering contracts: they contain superseded assumptions, constraints are often implicit, acceptance criteria are rarely executable, agents may overfit to recent turns, and reviewers cannot easily audit which instruction governed a change. The operational rule is that an agent should implement from a reviewed brief rather than from a long chat. The paper specifies that this structure becomes mandatory when a task affects public APIs, safety, security, performance, hardware behavior, regulated workflows, customer-facing behavior, shared libraries, or persistent data — while conversation remains appropriate for early uncertainty such as clarifying requirements, brainstorming architecture, and comparing test strategies, where the desired output is a better problem statement rather than code.

**A minimum input artifact model.** Seven categories of input are specified, each with distinct instantiations for software and for firmware or hardware: intent and scope, acceptance criteria, architecture context, constraints, execution context, evidence requirement, and risk class. Koch stresses that the goal is not to overload agents with context but to provide enough structured information to avoid guessing — a point he ties to the mixed empirical evidence on repository context files, from which he derives a minimal-context principle that instructions should be short, current, non-contradictory, and tied to executable feedback.

**Risk-adaptive acceptance gates.** Four levels are defined, from exploratory prototypes through routine changes and production changes to high-assurance domains such as security, payments, medical, firmware, and hardware. Each level specifies the required evidence and the corresponding human gate, ranging from optional review to explicit sign-off and a release gate. For production and high-assurance tasks the paper recommends a minimum evidence bundle comprising the task brief and requirement identifiers, the agent plan and affected files, executed commands and test results, a diff summary with residual risks, a trace from acceptance criteria to tests, the reviewer decision and follow-up actions, and a rollback or recovery path. The governing rule is that agent output is not accepted because it is plausible, but because it satisfies evidence appropriate to its risk level.

## Related Terms

The framework exists to counter [[DefinedTerm/verification-debt]], the condition in which agent output volume grows faster than a team's capacity to verify it. Its task-level loop is [[DefinedTerm/scope-v]]. Koch positions the whole framework as a move away from [[DefinedTerm/vibe-coding]] at scale and toward what he calls verified engineering with agents inside the loop.
