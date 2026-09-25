---
title: "How Anthropic teams use Claude Code"
type: "schema:Report"
lang: en
tags: [claude-code, ai-adoption, coding-agents, agentic-coding]
sources:
  - type: url
    url: 'https://www-cdn.anthropic.com/58284b19e702b49db9302d5b6f135ad8871e7658.pdf'
    hash: sha256:43cc7eca0261018e93d03fa4bfeef6d18bd52603938cdae9ed0719dfe22e2ea9
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An Anthropic document, drawn from interviews with the company's own Claude Code power users, describing how ten internal teams — from data infrastructure and security engineering to growth marketing, product design and legal — use Claude Code, what impact they report, and the tips they offer to other organizations considering adoption."
  publisher: "[[Organization/anthropic]]"
---

[[Organization/anthropic]] published this document to describe how its own internal teams use
[[SoftwareApplication/claude-code]]. It states that the insights were gathered through interviews
with the company's Claude Code power users, and presents them as covering how different departments
use the tool, its impact on their work, and tips for other organizations considering adoption.
Its framing claim is that the tool lets both developers and non-technical staff take on complex
projects, automate tasks and bridge skill gaps that had limited their productivity.

The document is organized by team, with ten sections: data infrastructure, product development,
security engineering, inference, data science and visualization, API, growth marketing, product
design, RL engineering, and legal. Each sets out the team's main use cases, the impact it reports and
its top tips. The figures it gives are the teams' own reports of time saved or output gained rather
than controlled measurements.

## Findings

- **Non-technical staff building and running tools.** Across several teams the reported change is
  that people without coding experience now do work that previously needed engineers. The data
  infrastructure team showed finance staff how to describe a data workflow in a plain text file and
  have Claude Code execute it; the growth marketing team, described as a non-technical team of one,
  built an agentic workflow with two specialized sub-agents that generates ad variations within
  character limits, a Figma plugin producing up to 100 ad variations per batch, and an MCP server for
  querying Meta Ads campaign data, and reports ad copy creation falling from 2 hours to 15 minutes and
  a tenfold increase in creative output; product designers implement visual and state-management
  changes themselves and report Figma and Claude Code being open 80% of the time; and the legal team
  built prototype tools, including a communication assistant for family members with speaking
  difficulties built in an hour.
- **Codebase navigation and onboarding.** Teams report using Claude Code to understand unfamiliar
  codebases instead of asking colleagues: new data scientists are directed to it to navigate a large
  codebase by reading its [[DefinedTerm/claude-md]] files, and the inference, API and security teams
  describe finding relevant files and understanding architecture quickly, with security engineers
  reporting contributions to existing projects within days instead of weeks.
- **Autonomy calibrated to the task.** The Claude Code team itself describes using auto-accept mode
  and autonomous loops, in which Claude writes code, runs tests and iterates, for prototyping and
  peripheral features, reviewing a roughly 80% complete result before taking over — and working
  synchronously with detailed prompts on core business logic. One asynchronous project, Vim key
  bindings, is reported as roughly 70% written by Claude's autonomous work. The team's tip is to learn
  which tasks suit asynchronous work and which need close supervision.
- **Checkpoints and restarts.** Several teams describe committing state before letting Claude work
  and reverting if it goes off track. The data science team likens this to a slot machine: commit,
  let it run for 30 minutes, then accept the result or start fresh, which it reports often succeeds
  more than trying to fix Claude's mistakes. The RL engineering team reports that a one-shot attempt
  works about one-third of the time and recommends trying one first before switching to a guided,
  collaborative approach.
- **Self-verification and tests.** The Claude Code team recommends setting Claude up to verify its
  own work by running builds, tests and lints, noting this is especially effective when Claude writes
  tests before code; security engineering describes guiding Claude through test-driven development in
  place of a pattern of "design doc → janky code → refactor → give up on tests"; and several teams
  use it to generate unit tests.
- **Instructions and reusable commands.** Teams recommend detailed CLAUDE.md files and adding
  instructions to prevent repeated tool-calling mistakes, and security engineering is reported to
  account for 50% of all custom slash command implementations in the monorepo
  ([[DefinedTerm/custom-slash-commands]]). The data infrastructure team recommends MCP servers over
  the BigQuery CLI for sensitive data, for tighter control over what Claude Code can access.
- **Reported time savings.** Security engineering reports infrastructure debugging falling from
  10–15 minutes of manual code scanning to about 5 minutes; the inference team reports research time
  on machine-learning concepts reduced by 80%, from an hour to 10–20 minutes; data science reports 2–4x
  savings on routine refactoring; and product design reports a launch-messaging change that would
  have taken a week of coordination completed in two 30-minute calls.
- **Limits noted by the teams.** The RL engineering team reports mixed results when debugging, and
  that Claude sometimes adds comments in odd places or organizes code questionably; the data science
  team observes that the model tends toward more complex solutions by default but responds well to
  requests for simpler ones; and the legal team, as product lawyers, flags the security implications
  of deep MCP integrations and expects conservative security postures to create barriers as AI tools
  reach more sensitive systems.
