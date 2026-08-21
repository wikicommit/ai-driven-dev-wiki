---
title: "Claude Code Advanced Patterns: Subagents, MCP, and Scaling to Real Codebases"
type: "schema:PresentationDigitalDocument"
lang: en
tags: [agentic-coding, configuration, agent-architecture, mcp]
sources:
  - type: url
    url: 'https://resources.anthropic.com/hubfs/Claude%20Code%20Advanced%20Patterns_%20Subagents,%20MCP,%20and%20Scaling%20to%20Real%20Codebases.pdf'
    hash: sha256:143e1a9f91063648c6ee3a39d9db2b5f2b9c7d42efa9188abdc46b3e3b104a9d
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An Anthropic webinar deck dated 24 March 2026 on scaling [[SoftwareApplication/claude-code]] to large codebases. It is organised around two decision tables — CLAUDE.md versus Hooks versus MCP for customization, and Parallel Claude versus Subagents versus Agent Teams for parallelization — followed by CI/CD integration and a live demo."
  datePublished: "2026-03-24"
  url: "https://resources.anthropic.com/hubfs/Claude%20Code%20Advanced%20Patterns_%20Subagents,%20MCP,%20and%20Scaling%20to%20Real%20Codebases.pdf"
---

"Claude Code Advanced Patterns: Subagents, MCP, and Scaling to Real Codebases" is a webinar slide deck published by [[Organization/anthropic]] and dated 24 March 2026. The deck credits no individual presenter; its housekeeping slide indicates a live session with a Q&A tab and a follow-up recording, and several slides are marked CONFIDENTIAL.

The deck states five learning outcomes: controlling Claude's behavior with CLAUDE.md and Hooks, parallelizing Claude for productivity, embedding Claude Code across the SDLC from feature research to CI/CD, forming a mental model for when tool creation is worth the cycles, and imagining what an advanced implementation could look like for an organization. Its structure follows those outcomes as three sections — customizing, parallelizing, embedding. The first two each close with a "When to use which feature" table that assigns each mechanism a distinct condition of use rather than ranking them; the embedding section instead holds the GitHub Actions and Code Review slides, and is followed by a live demo.

Because this is a slide deck rather than prose, much of its content is compressed into short table cells; what follows records only what the slides themselves assert.

## Key Points

- **CLAUDE.md is described as "similar to a README, but for Claude"** — a forced README file giving Claude instructions on project structure, common commands, and personal styling tips. For large codebases the deck shows a hierarchical arrangement in which Claude walks up the directory tree to discover CLAUDE.md files, with a monorepo-root file holding system overview, modernization strategy, and team structure, a `/packages/` file holding component architecture, technical debt, and migration plans, and per-package files below that.
- **Three CLAUDE.md practices for large codebases.** Keep files under 200 lines, on the stated grounds that longer files consume more context and can negatively affect instruction adherence; organise instructions into multiple files under a `.claude/rules/` directory, where rules can be scoped to specific file paths through a `paths` field in the frontmatter; and use the `claudeMdExcludes` setting to exclude CLAUDE.md files irrelevant to a project so they cannot contribute contradictory instructions. The deck notes that managed-policy CLAUDE.md files cannot be excluded.
- **A three-way customization decision.** CLAUDE.md is for project-related context and instructions that prevent repeating oneself ("use pnpm, not npm. Run tests with pytest. Follow PEP8."); [[DefinedTerm/agent-hooks]] are for deterministic automation that must always run at specific lifecycle events (auto-format on save, run tests after edits, send notifications on completion); and [[DefinedTerm/model-context-protocol]] is for access to external tools, databases, and APIs through a standardized protocol (query a database, fetch from GitHub, send Slack messages, access Google Drive). The deck gives `mcp add <server-name>` as the way to add a server, and states MCP's ideal use case as Claude needing to reason over external state — fetching Figma designs, creating tickets — without relying on copy and paste.
- **A three-way parallelization decision.** Parallel Claude means running multiple Claude Code instances simultaneously, each in its own terminal with its own context, working on separate unrelated tasks; the deck names git worktrees as the isolation mechanism and gives `claude --worktree` as the way to create one. [[DefinedTerm/subagents]] are for delegating focused subtasks from the main session with isolated context. Agent Teams are for splitting one large task into independent workstreams that coordinate.
- **Three stated conditions for reaching for a subagent.** When the subagent can be given a clear and relatively specialized role with defined tool access levels and criteria for success or completion; when inspecting or interacting with the subagent's work is not a priority and only a completed task and a few conclusions are needed; and to manage the main session's context. The deck gives the ideal use case as parallel experimentation or investigation of the codebase requiring only a lighter amount of information returned to the main agent, and shows subagents as Markdown files in an `agents/` directory alongside CLAUDE.md.
- **Agent Teams are described as being in research preview** at the time of the deck: multiple agents that communicate, coordinate, and divide-and-conquer parallelized work, said to shine when a task can be broken into independent workstreams so each agent can own a slice without blocking others.
- **Two CI/CD integrations.** Claude Code in GitHub Actions, described as powered by the Claude Agent SDK, allows remotely triggering edits to pull requests and issues by tagging `@claude`, and is set up by running `/install-github-app` from within Claude Code. Code Review is described as an agent-team-based review system whose specialized agents have context on the full codebase, post inline comments on bugs and security gaps rated by severity, and are aimed at finding easy-to-miss edge cases and regressions; enabling it is an admin action involving the Claude Code settings, the GitHub App, and per-repository opt-in.

## Context

The deck closes with a live demo framed as three time-consuming tasks tackled simultaneously: adding an @mention feature to a ticketing tool, deciding priorities and assigning tickets for a sprint, and getting through an initial code review for a major addition. That framing — three unrelated tasks at once — is the deck's own illustration of the Parallel Claude row of its parallelization table.

As a vendor deck about the vendor's own product, its recommendations are Anthropic's account of how it intends Claude Code to be used, not independent evaluation. Its content overlaps substantially with the written Claude Code documentation already recorded on [[SoftwareApplication/claude-code]]; what the deck adds beyond that is the explicit side-by-side decision framing and the CLAUDE.md sizing and exclusion practices.
