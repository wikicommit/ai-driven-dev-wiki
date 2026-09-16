---
title: "Agent Teams"
type: "schema:DefinedTerm"
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
  description: "Claude Code's experimental feature for true parallel multi-agent execution: a shared task list with dependency tracking and file locking, plus direct peer-to-peer messaging between teammates, coordinated by a team lead."
---

Agent Teams is an experimental Claude Code feature for running several agents on a task in true parallel, adding coordination primitives that a plain subagent setup lacks. It is enabled with the environment variable `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` and structures work across three layers: a Team Lead that decomposes work, creates the task list, and synthesizes results; a shared task list tracking each task's status (pending, in-progress, completed, blocked) with dependency tracking and file locking; and teammates — each an independent Claude Code instance with its own context window, running in separate tmux panes — that self-claim tasks from the list.

## Usage

Teammates message each other directly rather than routing through the lead, so when one finishes a task and marks it complete, any tasks that depended on it automatically unblock without the lead acting as an intermediary. File locking prevents two teammates from editing the same file at once. A reported practice is spawning a dedicated, read-only "@reviewer" teammate — restricted to lint, test, and security-scan tools and triggered automatically on every task completion — so that the lead only ever integrates already-reviewed code.

## Related Terms

[[SoftwareApplication/claude-code]], [[DefinedTerm/sub-agent-architecture]]
