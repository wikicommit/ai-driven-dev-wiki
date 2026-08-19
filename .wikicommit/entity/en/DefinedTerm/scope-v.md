---
title: "SCOPE-V"
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
  description: "The task-level execution loop of the Agentic Agile-V framework, comprising six steps — Specify, Constrain, Orchestrate, Prove, Evolve, and Verify — through which an individual agentic task is run."
---

SCOPE-V is the task-level execution loop of the [[DefinedTerm/agentic-agile-v]] framework proposed by Christopher Koch. Where the framework's macro layer, Agile-V, governs the lifecycle of an increment, SCOPE-V governs how an individual agentic task is run, passing it through six named steps.

## Usage

| Step | What it covers |
| --- | --- |
| **S**pecify | Convert intent into a task brief with objective, scope, non-goals, affected modules, dependencies, acceptance criteria, and required evidence |
| **C**onstrain | Define boundaries — no public API change unless approved, no unrelated files, no new dependencies without justification, no broad refactor during a bug fix, explicit review for security-sensitive code, and mandatory preservation of hardware timing and safety constraints |
| **O**rchestrate | Define how the agent should work: inspect first, summarize current design, propose a plan, implement small slices, run local checks, and produce a diff summary with residual risks |
| **P**rove | Require evidence appropriate to risk — unit, integration, and regression tests, static analysis, type checks, linting, security scans, simulation, formal checks, hardware-in-the-loop results, or review checklists |
| **E**volve | Feed validated learning back into repository instructions, templates, tests, and engineering baselines, and remove stale or harmful instructions |
| **V**erify | Treat verification as recurring rather than final: before implementation, during patching, before merge, after deployment, and after field feedback |

The last step is the one [[ScholarlyArticle/agentic-agile-v]] emphasizes as a departure from convention. Rather than a terminal quality gate, verification recurs throughout — a position the paper reinforces in its guidance on testing, where it argues testing must be inside the agent loop rather than after it: identifying expected tests, edge cases, and failure modes before implementation; running targeted tests after small changes during implementation; requiring CI, static analysis, type checks, security checks, and review before merge; and monitoring logs, defects, performance, and user feedback after merge.

The Orchestrate step's "inspect first, then plan, then implement" ordering appears again in the paper's task-specific workflows. For feature development it recommends writing a feature brief, identifying affected modules and tests, asking the agent to inspect and summarize the current design, requiring a plan before edits, implementing the smallest useful slice, adding or updating tests alongside implementation, running targeted and regression checks, producing an evidence bundle and residual-risk note, and requiring human review for architecture, security, maintainability, and edge cases. For bug fixing — which the paper frames as causal diagnosis rather than feature generation — it recommends that the agent should not patch immediately, but instead capture observed and expected behavior, supply reproduction steps and environment details, propose hypotheses and name missing evidence, localize likely files and call paths, create a failing regression test where possible, apply the minimal patch, run regression and nearby tests, and explain why the fix works and what it does not address.

## Related Terms

SCOPE-V is the micro layer of [[DefinedTerm/agentic-agile-v]]; its Prove and Verify steps are the framework's direct answer to [[DefinedTerm/verification-debt]].
