---
title: "Agent-driven development in Copilot Applied Science"
type: "schema:BlogPosting"
lang: en
tags: [agentic-engineering, coding-agents, guardrails]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/agent-driven-development-in-copilot-applied-science/'
    hash: sha256:900fe932178827ecd6df3b0cd594d93c22c0e9cd960bd539ec89b97b0a9e6ed3
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A firsthand account from GitHub's Copilot Applied Science team of building an agent tool with coding agents as the primary contributor, distilled into prompting, architectural and iteration principles and a plan-implement-review loop."
  author: ["Tyler McGoffin"]
  datePublished: "2026-03-31"
  publisher: "[[Organization/github]]"
---

A post on GitHub's blog by a senior applied researcher on the Copilot Applied Science team, who
analyses coding-agent performance against benchmarks such as [[Dataset/terminal-bench]] and
[[Dataset/swe-bench-pro]]. That work means reading agent trajectories — the records of the reasoning
and actions an agent takes on each task — in volumes the author puts at hundreds of thousands of lines.
Having repeatedly used [[SoftwareApplication/github-copilot]] to surface patterns before investigating
them by hand, the author automated that loop as `eval-agents`, a tool for building and sharing agents
that do the analysis.

The post's argument is less about that tool than about how it was built. Its design goal was to make
coding agents the project's primary contributor, and the author reports that setting the project up
for that also made it easier for people to use and extend. The recurring claim is that what makes
human engineers effective — clear context, clean architecture, tests, documentation, guardrails — is
what makes coding agents effective too.

## Key Points

- The author's setup was [[SoftwareApplication/github-copilot-cli]] with Claude Opus 4.6 in VS Code,
  with the Copilot SDK (which the post says is powered by Copilot CLI) supplying existing tools, MCP
  servers, and a way to register new tools and skills.
- Prompting: the post recommends being conversational and verbose and using a planning mode before
  an agent mode — treating the agent like an engineer by guiding its thinking and over-explaining
  assumptions, rather than giving it a terse problem statement.
- One example: prompted in planning mode about Copilot rewriting tests to fit its own changes, the
  author arrived with Copilot at guardrails akin to contract testing that only humans can update.
- Architecture: refactoring, documentation, test-writing and dead-code cleanup become the most
  important work in an agent-first repository, because they are what let the agent navigate the
  codebase; the author says delivering features becomes trivial once that groundwork is in place.
- Iteration: the author has moved from "trust but verify" to "blame process, not agents", modelled
  on blameless culture — when the agent makes a mistake, add tests, better prompts or other
  guardrails so it cannot repeat it. Strict typing, robust linters and integration, end-to-end and
  contract tests are presented as the means by which the agent checks its own work.
- The development loop proposed: plan the feature with `/plan` (including tests, and documentation
  updates done before code); implement it on `/autopilot`; have Copilot run a review loop with the
  Copilot Code Review agent until no relevant comments remain; then do a human review.
- Outside that loop, the author runs recurring `/plan` prompts — for missing or broken tests and dead
  code, for duplication, and for documentation gaps including `copilot-instructions.md` — weekly on a
  schedule and often more frequently.
- The reported outcome: with five people joining the project for the first time, the team created 11
  new agents, four new skills and a concept of eval-agent workflows in less than three days, a change of +28,858/−2,884 lines across 345 files.
  This is the author's own account of their team's work, not a measured comparison.

## Context

The post frames coding agents through a junior-engineer analogy throughout — onboard them well, give
them context, build guardrails so mistakes do not become disasters — and closes by arguing that the
technology is new but the principles are not. It sits alongside other writing on preparing a
codebase for agents, such as [[DefinedTerm/agents-md]]-style instruction files and
[[DefinedTerm/guardrails]]. Its evidence is one team's experience on an internal tool, written by
someone at the vendor of the tools it recommends.
