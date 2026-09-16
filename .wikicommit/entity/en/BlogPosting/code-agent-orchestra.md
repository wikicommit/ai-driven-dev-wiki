---
title: "The Code Agent Orchestra - what makes multi-agent coding work"
type: "schema:BlogPosting"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/code-agent-orchestra/'
    hash: sha256:f16aa303da51395585e293ea9d466a00847210974b774f822827f13f48b30431
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A write-up of a conference talk arguing that AI-assisted coding is shifting from a single synchronous agent to orchestrating multiple asynchronous agents, and setting out the patterns, tools, and quality gates needed to do that reliably."
  author: "Addy Osmani"
  datePublished: "2026-03-26"
---

This post is a write-up of a talk given at O'Reilly AI CodeCon, arguing that AI-assisted coding is shifting from a "conductor" model — one agent, guided synchronously, bounded by a single context window — to an "orchestrator" model, where a developer coordinates multiple asynchronous agents each with their own context window and file scope. It sets out three escalating multi-agent patterns (subagents, [[DefinedTerm/agent-teams]], and orchestration platforms at scale), the quality gates needed to trust their output, and a "factory model" for running the resulting workflow as a production line.

The post argues the bottleneck in this shift has moved from code generation to verification, and that the discipline required — clear specs, quality gates, and knowing what to keep for yourself versus delegate — determines whether an "army of agents" compounds progress or compounds mistakes.

## Key Points

- Three single-agent constraints motivate going multi-agent: context overload (large codebases overwhelm one context window), no specialization (a generalist agent writes worse code than a focused one), and no coordination (spawned helpers can't share a task list or resolve dependencies).
- [[DefinedTerm/agent-teams]], Claude Code's experimental feature, adds a shared task list with dependency tracking and peer-to-peer messaging between teammates, which the post credits with solving the coordination problem subagents alone leave unsolved.
- The post reports a three-tier landscape of orchestration tools in 2026: in-process subagents/teams (single terminal, no extra tooling), local orchestrators such as Conductor, Vibe Kanban, and Claude Squad (3-10 agents in isolated worktrees with dashboards), and cloud async agents such as Claude Code Web, GitHub Copilot Coding Agent, and Jules (assign a task, return to a pull request).
- It states that three to five teammates is reported as the sweet spot for Agent Teams, since token costs scale linearly with team size and focused smaller teams are reported to outperform larger scattered ones.
- It recommends a dedicated, read-only "@reviewer" teammate (running Claude Opus 4.6, restricted to lint/test/security-scan tools) triggered automatically on every task completion, so the lead only ever integrates already-reviewed code.
- It describes the [[DefinedTerm/ralph-loop]] pattern (attributed to Geoffrey Huntley and Ryan Carson) as a five-step pick/implement/validate/commit/reset cycle for autonomous overnight development, with safeguards including killing and reassigning an agent stuck for 3+ iterations and per-role token budgets.
- Citing research on AGENTS.md (Gloaguen et al., ETH Zurich), it reports that LLM-generated AGENTS.md files offer no benefit and can reduce success rates by roughly 3% while increasing inference cost by over 20%, versus a roughly 4% improvement from developer-written context files.
- It proposes a six-step "factory model" production line for agentic development — Plan, Spawn, Monitor, Verify, Integrate, Retro — with practical limits such as capping work-in-progress at 3-5 agents and defining kill criteria for stuck agents.
- It argues the quality of a spec is the main lever on output quality at scale: a vague spec's errors multiply across a whole fleet of parallel agents, while a precise one multiplies into precise implementations.

## Context

The post links to the author's separate writing on spec quality and on a "factory model" of agentic development as further reading for topics it touches on, and cites Steve Yegge's eight-level ladder of AI-assisted coding as the framework the talk's material (levels 5 through 8) builds on, without restating what each of those levels is.
