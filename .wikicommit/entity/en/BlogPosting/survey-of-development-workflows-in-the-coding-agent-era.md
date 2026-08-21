---
title: "A Survey of Development Workflows in the Coding Agent Era"
type: "schema:BlogPosting"
lang: en
tags: [agentic-engineering, workflow, context-engineering, survey]
sources:
  - type: url
    url: 'https://nyosegawa.com/en/posts/coding-agent-workflow-2026/'
    hash: sha256:bb7d36388cc5d0dc91fc90185585f6fff68833b1b198e732c6e2d6d41a285f45
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A practitioner survey of coding-agent development practice as of March 2026, organised into project workflows, in-session quality techniques, and supporting infrastructure, closing with the author's own idea-driven and automated workflows."
  author: "逆瀬川ちゃん"
  datePublished: "2026-03-14"
  publisher: ""
---

This post surveys how development is actually run in the coding-agent era, organising the state of the field as of March 2026 into three layers — how to run projects, techniques for coding with agents, and the infrastructure that supports both — and closing with the author's own workflow. It positions itself as the sequel to an earlier post on harness engineering, which it treats as the implementation foundation this one zooms out from.

Its framing concept is [[DefinedTerm/agentic-engineering]]. The post reports that Karpathy proposed vibe coding in February 2025, that it matured over the following year into a structured engineering methodology, and that in February 2026 Karpathy renamed it agentic engineering — with the definition that you do not write code directly and 99% of your time goes to orchestrating and supervising the agents that do.

## Key Points

**Four project workflows** are presented as combinable rather than mutually exclusive.

- **Brainstorm → Plan → Execute (Harper Reed style)** — a conversational LLM prompted to *ask me one question at a time* produces `spec.md`, a reasoning model turns it into `prompt_plan.md` and `todo.md`, and the prompts are fed to an agent in order. Best suited to greenfield personal projects, which the post says Harper acknowledges himself; its importance is having established the principle of not jumping straight to code.
- **[[DefinedTerm/spec-driven-development]] / AI-DLC** — the fastest-spreading workflow between 2025 and 2026, positioned as the antithesis of vibe coding, with a basic flow of Requirements → Design → Tasks → Implementation. The post cites a three-level classification of SDD into spec-first, spec-anchored and spec-as-source, and a Technology Radar rating of Assess. AWS's AI-DLC extends it to team and organisation scale across Inception, Construction and Operations phases, with a four-hour synchronous Mob Elaboration session converting business intent into detailed requirements, and an Adaptive Workflow that picks stages from a nine-stage menu by task complexity. Its stated benefit is replacing micro-approvals during implementation with phase-gate reviews, fixing approval fatigue; its stated problems are spec drift from code — "drowning in a sea of markdown" — overkill for small bug fixes, and a risk of regressing to heavy upfront specs plus big-bang releases.
- **[[DefinedTerm/research-plan-implement]]** — a three-phase workflow whose core rule is that the agent writes no code until a detailed written plan has been reviewed and approved.
- **[[SoftwareApplication/superpowers]]** — a skill framework that encodes SDD and TDD into a single seven-stage pipeline and forces the methodology on the agent.

Its selection guide is greenfield solo work → Harper Reed; teams needing spec management → SDD; large changes to existing codebases → RPI; whole-workflow automation → Superpowers.

**In-session quality techniques.** [[DefinedTerm/context-engineering]] is named the single most important lever, ahead of model choice, with techniques for context packing, [[DefinedTerm/progressive-disclosure]], using the filesystem as external memory, managing attention with a `todo.md` re-injected at the end of context, and deliberately *not* erasing failure states so the agent does not repeat a mistake. Two anti-patterns are named: loading context files with many few-shot examples, which makes the agent imitate patterns instead of thinking, and filling the context window before work starts. Further sections cover [[DefinedTerm/context-rot]], TDD with coding agents, [[DefinedTerm/multi-agent-orchestration]], the [[DefinedTerm/best-of-n]] parallel strategy, AI-on-AI review, failure modes, and agent-native code design.

**A failure-mode table** pairs six symptoms with mitigations: hallucination (inject current docs, catch via tests), infinite loop (gutter detection, token-limit termination), over-generation (limit scope explicitly, write prohibitions into the context file), false completion (auto-run tests via a PostToolUse hook), agent drift (correct mechanically with linters and type checkers), and probabilistic cascade — 95% success per step becoming 77% over five — mitigated by smaller tasks verified individually.

**Agent-native code design** is offered as prior to technique: grep-able naming with named exports and consistent error types, collocated tests under a consistent naming convention so a single `ls` confirms their existence, feature-level rather than horizontal modularisation, tests treated as the reward signal that tells an agent whether an implementation is correct, and interface contracts agreed upfront as a prerequisite for parallel multi-agent work.

**Infrastructure.** Sections cover designing context files, the [[DefinedTerm/agent-skills]] and plugin ecosystem, hooks and linters as the deterministic layer, git worktrees as the physical foundation for parallelism, the MCP-versus-CLI-plus-skills question, an orchestration tool landscape sorted into workflow-definition, agent-management, process-multiplexer and role-based types, long-session design, [[SoftwareApplication/github-agentic-workflows]], security, and [[SoftwareApplication/symphony]].

**The author's own practice** mixes patterns rather than adopting one. An *idea-driven* flow runs idea → agent-drafted spec → user review → agent implementation → user acceptance, with a Patrol Agent periodically checking for stalled sessions and batching notifications so the user handles them in bursts rather than being interrupted continuously. An experimental *automated* flow prepares exhaustive development docs, sets up the harness and feedback loop, writes tasks into `tasks.jsonl`, and lets the agent run plan-mode → auto-approve → implement per task with an automatic review on commit hook; the post reports an eight-hour automated run completing on that setup.

## Context

This is a practitioner survey rather than research: most of its figures — star counts, benchmark scores, reported speedups — are relayed from the sources it links rather than measured by the author, and it says so by citing each. Its own contribution is the organisation into three layers and the selection guidance between workflows.

Its stated summary is that agentic engineering is established in 2026, that development is designed across project workflows, implementation techniques and infrastructure, and that what really matters is closing the feedback loop deterministically, inserting humans at structured points, and keeping sessions short.
