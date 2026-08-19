---
title: "Claude Code"
type: "schema:SoftwareApplication"
lang: en
tags: [agentic-coding, cli, ai-assisted-programming]
sources:
  - type: url
    url: 'https://arxiv.org/html/2602.14690v1'
    hash: sha256:a95102e253d7131ba8bf5f38f7f1e738784be17159af65fa612395d8ed4800b9
  - type: url
    url: 'https://code.claude.com/docs/en/best-practices'
    hash: sha256:92807ef3d58f63fbea435ea928df49e2f3341e118eb8c40db08800c100a4c4c5
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
    hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be
  - type: url
    url: 'https://sddbook.blob.core.windows.net/downloads/spec-driven-development.pdf'
    hash: sha256:7f897827f00db69ac4a15f3acea3826e5504b1600d0b785cdce210d5414f1eea
  - type: url
    url: 'https://code.claude.com/docs/en/hooks-guide'
    hash: sha256:155e5ab620eab496f8385a3e87ca54687af20c5b57321f14baee4017a74188b1
  - type: url
    url: 'https://code.claude.com/docs/en/skills'
    hash: sha256:0a1bf9dee2f0ff1bb9f2ab54bbdd859d458c6bc13d2159e42d3ced61ce360a94
  - type: url
    url: 'https://code.claude.com/docs/en/sub-agents'
    hash: sha256:12cc07fa94c1e50e47e202b2d565884e44401d3bce47e2e2c8dc5598cb57f87a
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An agentic AI coding tool with a command-line interface, released in February 2025. A February 2026 study of 2,926 GitHub repositories found it the most frequently present of five major agentic coding tools, and the one whose repositories employ the broadest range of configuration mechanisms."
  applicationCategory: "Agentic AI coding tool (CLI)"
---

Claude Code is an agentic AI coding tool with a command-line interface, released in February 2025 with its CLI and agents available from launch. [[ScholarlyArticle/configuring-agentic-ai-coding-tools]] treats it as one of five major agentic coding tools, and its adoption study found Claude Code the most widely present of them: it appeared in 1,310 of the 2,926 sampled GitHub repositories that use any such tool.

Unlike purely reactive conversational assistants, agentic tools of this kind take initiative to accomplish defined objectives, autonomously interacting with development environments and using project artifacts, external data, and command-line tools. Claude Code was among the first tools to implement a central agent loop of this shape.

## Overview

The study characterises Claude Code as having the broadest configuration footprint of the tools examined — its users employ the widest range of repository-level configuration mechanisms. Repositories adopting it were also the most likely to appear in combination with another tool; the most common pairing observed was Claude Code with [[SoftwareApplication/github-copilot]], in 128 repositories.

## Features

Claude Code exposes seven of the eight configuration mechanisms catalogued in the study, each backed by a repository-level artifact:

- [[DefinedTerm/context-files]] — `CLAUDE.md`, the most common context file type in the sample at 1,661 files and present in 45.4% of repositories
- Settings — `.claude/settings.json` and `.claude/settings.local.json`
- [[DefinedTerm/agent-skills]] — `.claude/skills/`
- [[DefinedTerm/subagents]] — `.claude/agents/`
- Commands — `.claude/commands/`
- Hooks — defined within `.claude/settings.json`
- MCP servers — `.mcp.json`

It does not offer the Rules mechanism, which the study notes is concentrated instead in [[SoftwareApplication/cursor]] repositories. One capability specific to Claude Code's subagents is that they can have their own persistent memory directory, surviving across interactions and usable to accumulate knowledge such as debugging insights — though the study found no repositories in its sample actually storing such memory files.

Anthropic's own documentation adds the session and scaling controls that sit above those configuration artifacts. **Plan mode** (`Shift+Tab`, or `claude --permission-mode plan`) separates exploration from execution, and the documentation recommends a four-phase workflow of explore, plan, implement, commit — while noting the overhead is not worth it when the scope is clear: "if you could describe the diff in one sentence, skip the plan." **Permission modes** determine how much is approved by a human: auto mode, the built-in starting mode for interactive terminal and VS Code sessions on Pro, Max, and Team plans, has a separate classifier model review most actions and block only what looks risky, such as scope escalation, unknown infrastructure, or hostile-content-driven actions; Manual mode, the starting mode on other plans, asks before file writes, Bash commands, and MCP tools, with permission allowlists and OS-level sandboxing available to cut the interruptions. **Checkpointing** snapshots files before each change so `/rewind` (or double-tapping `Escape`) can restore conversation, code, or both — with the documented limitation that only changes made through the file editing tools are tracked, so Bash and external processes are not covered and it is not a replacement for git. **Sessions** are saved locally and resumable with `claude --continue` or `claude --resume`, and can be named with `/rename`. **Non-interactive mode** (`claude -p`) supports plain text, JSON, and streaming JSON output for CI, pre-commit hooks, and fan-out loops over many files. For parallel work the documentation lists worktrees, the desktop app, Claude Code on the web, and agent teams.

Anthropic's own documentation organises those artifacts into four named extension points and cross-references them as alternatives to each other: [[DefinedTerm/agent-skills]] for giving the model additional instructions and executable commands, [[DefinedTerm/subagents]] for running tasks in isolated contexts, [[DefinedTerm/agent-hooks]] for deterministic automation at lifecycle events, and plugins for packaging extensions to share across projects.

Two of those ship with populated defaults. A set of **bundled skills** is available in every session — the documentation names `/doctor`, `/code-review`, `/batch`, `/debug`, `/loop`, and `/claude-api`, and separately a trio of `/run`, `/verify`, and `/run-skill-generator` that exist to launch a project's app and confirm a change against the running app rather than against tests alone, with `/run-skill-generator` recording the working launch recipe as a per-project skill so later runs and other agents follow it instead of rediscovering it. A `disableBundledSkills` setting turns them all off except `/doctor`. There are also **built-in subagents** the model delegates to automatically: Explore, a read-only agent for file discovery and code search that is invoked with a stated thoroughness level; Plan, the read-only research agent used during plan mode; general-purpose, which has every tool available to subagents; and helper agents including a catch-all `claude`, `statusline-setup`, and `claude-code-guide`.

[[TechArticle/effective-context-engineering-for-ai-agents]] describes how Claude Code manages context internally. It is given as the worked example of just-in-time retrieval: the model writes targeted queries, stores results, and uses Bash commands such as `head` and `tail` to analyse large volumes of data without loading full objects into context. It is also given as the example of a hybrid strategy — `CLAUDE.md` files are dropped into context up front, while glob and grep retrieve files just in time, which the post argues bypasses the problems of stale indexing and complex syntax trees. Its [[DefinedTerm/compaction]] implementation passes the message history to the model to summarise, preserving architectural decisions, unresolved bugs, and implementation details while discarding redundant tool outputs, and continues from that summary plus the five most recently accessed files.

## Recommended practice

Anthropic publishes a best-practices guide whose recommendations are organised around a single stated constraint: the context window fills up fast and performance degrades as it fills, which the guide calls the most important resource to manage. Its headline recommendations are to give the agent a check it can run — a test suite, build exit code, linter, fixture diff, or browser screenshot — described as "the difference between a session you watch and one you walk away from," because without one, "looks done" is the only stop signal available and the human becomes the verification loop; and to have the agent show evidence, such as test output or the command it ran, rather than asserting success.

The guide escalates that check through four levels of enforcement: asking for it in the prompt, setting it as a `/goal` condition re-evaluated after every turn, wiring it as a Stop hook that blocks the turn from ending, or having a second model refute the result. It also recommends managing context aggressively (`/clear` between unrelated tasks, `/compact` with instructions, `/btw` for questions that should not enter history), delegating investigation to [[DefinedTerm/subagents]] so exploration does not consume the main context, and adding an adversarial review step in a fresh subagent context before treating work as done.

Its list of common failure patterns is unusually concrete: the "kitchen sink session," where unrelated tasks fill context with irrelevant information; correcting over and over, for which the prescribed fix is that after two failed corrections you should `/clear` and write a better prompt incorporating what you learned; the over-specified `CLAUDE.md`, where important rules get lost in the noise; the trust-then-verify gap, where a plausible-looking implementation does not handle edge cases; and infinite exploration, where an unscoped investigation reads hundreds of files. The guide closes by framing all of this as starting points rather than rules, and encourages users to develop their own intuition about when to plan, when to explore, and when to let context accumulate.

## History

Claude Code was released in February 2025. As of the study's February 2026 snapshot, the authors note it did not yet support [[DefinedTerm/agents-md]], the tool-agnostic context file convention their data identifies as the emerging cross-tool standard; they offer this as one possible explanation for the observed creation-order pattern, in which CLAUDE.md appears first and AGENTS.md is added later. Separately, CLAUDE.md pointing to AGENTS.md was the single strongest reference pattern in their data, occurring 311 times. Repositories using Claude Code had a median age of 6.2 years, slightly younger than the sample as a whole.

[[Book/spec-driven-development-ai-native-software-engineering]] tracks a separate measure of the project's maturity: how much of Claude Code is written by Claude Code. [[Person/boris-cherny]], who leads the project at [[Organization/anthropic]], reported in May 2025 that roughly 80% of it was; by October, Dario Amodei told Marc Benioff the number was above 90%; and on 7 March 2026 Cherny posted publicly, "Can confirm Claude Code is 100% written by Claude Code." [[Person/kevin-ryan]] cites that progression — eighty to one hundred percent in ten months — alongside a report that OpenAI's Codex 5.3 was built by Codex itself, as evidence that "the recursive loop is closed."
