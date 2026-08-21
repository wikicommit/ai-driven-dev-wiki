---
title: "The Code Agent Orchestra - what makes multi-agent coding work"
type: "schema:BlogPosting"
lang: en
tags: [multi-agent, agentic-coding, orchestration, quality-gates]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/code-agent-orchestra/'
    hash: sha256:399fcd256a0dea0d4dc0841558f7f17cf41a9b447bc6bbc5adfbaf8728e9c557
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A write-up by Addy Osmani of his March 2026 O'Reilly AI CodeCon talk on coordinating multiple coding agents, covering three multi-agent patterns, a three-tier tool landscape, and the quality gates the author argues make agent output trustworthy."
  author: "[[Person/addy-osmani]]"
  datePublished: "2026-03-26"
  publisher: ""
---

"The Code Agent Orchestra - what makes multi-agent coding work" is [[Person/addy-osmani]]'s written version of a talk he gave at O'Reilly AI CodeCon on 26 March 2026. Its organising claim is that a shift has already happened in how productive developers work: from a *conductor* model, where one developer guides a single agent synchronously and the context window is a hard ceiling, to an *orchestrator* model, where several agents run asynchronously, each with its own context window and file scope, while the developer plans and checks in from above.

The post is structured as three escalating patterns — [[DefinedTerm/subagents]], Claude Code's [[DefinedTerm/agent-teams]] feature, and purpose-built orchestration tooling — followed by the quality gates the author argues are what make the whole arrangement trustworthy. Alongside those recommendations it carries a warning: that the human bottleneck was "a feature, not a bug," because at human pace mistakes are felt early, whereas an orchestrated fleet compounds small errors faster than a developer can catch them. The post itself ends on five patterns to start with, beginning with subagents.

## Key Points

- **Three constraints define the single-agent ceiling**: context overload, no specialisation, and no coordination. The post's claim is that subagents solve the first two and Agent Teams solve all three.
- **Four compounding reasons to go multi-agent**: parallelism (the post gives "3x throughput" for three agents on frontend, backend and tests), specialisation through narrow file ownership, isolation via git worktrees, and compound learning accumulated in an [[DefinedTerm/agents-md]] file.
- **Hierarchical delegation over wide fan-out**: rather than one orchestrator spawning six subagents and fragmenting its own context, spawn two feature leads that each decompose their own brief. Osmani compares this to tech-lead layers in an engineering organisation.
- **A three-tier tool landscape for 2026**: Tier 1 in-process subagents and Agent Teams; Tier 2 local orchestrators running isolated worktrees with dashboards and diff review (best for 3–10 agents); Tier 3 cloud async agents that return a pull request. He expects most developers to use all three.
- **Three to five teammates is the stated sweet spot**, with token costs scaling linearly with team size.
- **Three quality gates**: plan approval before implementation, hooks that run automated checks on lifecycle events (a `TaskCompleted` hook running lint and tests, a `TeammateIdle` hook verifying tests pass), and `AGENTS.md` as the vehicle for compound learning.
- **Verification, not generation, is the bottleneck** — see [[DefinedTerm/verification-bottleneck]]. The post's specific argument is that passing tests do not guarantee regression coverage, that agents write tests that are valid but miss what matters, and that a flaky environment one developer treats as an annoyance becomes a systemic blocker when forty agents hit it simultaneously.
- **Delegate the tasks, not the judgment**: agents are suited to work with a tight evaluation function — boilerplate, migrations, test scaffolding — while architecture, deciding what not to build, and reviewing with full system context stay with the developer.
- **The spec is the leverage**: with fifty agents in parallel, an ambiguous requirement propagates through dozens of runs each going wrong differently, which is the post's explanation for why strong engineers get *more* leverage from these tools rather than less.

## Context

The post is a talk write-up rather than a research result, and most of its claims are presented as the author's own practice and observation. Where it does reach for external evidence it says so: Osmani cites research by Gloaguen et al. at ETH Zurich for the claim that LLM-generated `AGENTS.md` files offer no benefit and can marginally reduce success rates (roughly 3% on average) while increasing inference costs by over 20%, whereas developer-written context files give a modest improvement of around 4% — which is the basis for his rule that the lead must approve every line and an agent should never write to `AGENTS.md` directly.

It also frames Steve Yegge's eight levels of AI-assisted coding as the ladder the talk is positioned on, covering levels 5 through 8, without restating what the individual levels are. Several of the post's own sections are summaries of longer pieces the author has published separately; this page records only what this post itself states.
