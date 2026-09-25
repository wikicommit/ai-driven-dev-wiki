---
title: "Agent Teams"
type: "schema:DefinedTerm"
lang: en
aliases: ["Claude Code swarms"]
tags: [multi-agent]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/code-agent-orchestra/'
    hash: sha256:f16aa303da51395585e293ea9d466a00847210974b774f822827f13f48b30431
  - type: url
    url: 'https://addyosmani.com/blog/claude-code-agent-teams/'
    hash: sha256:b36f513e61d7ef1ac90ab862218ac5db53654893d583aba69626a3e5ac82e049
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Claude Code's experimental feature for true parallel multi-agent execution: a shared task list with dependency tracking and file locking, plus direct peer-to-peer messaging between teammates, coordinated by a team lead."
---

Agent Teams is an experimental Claude Code feature for running several agents on a task in true parallel, adding coordination primitives that a plain subagent setup lacks. It is enabled with the environment variable `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` and structures work across three layers: a Team Lead that decomposes work, creates the task list, and synthesizes results; a shared task list tracking each task's status (pending, in-progress, completed, blocked) with dependency tracking and file locking; and teammates — each an independent Claude Code instance with its own context window, described in [[BlogPosting/code-agent-orchestra]] as running in separate tmux panes — that self-claim tasks from the list.

## Usage

Teammates message each other directly rather than routing through the lead, so when one finishes a task and marks it complete, any tasks that depended on it automatically unblock without the lead acting as an intermediary. File locking prevents two teammates from editing the same file at once. A reported practice is spawning a dedicated, read-only "@reviewer" teammate — restricted to lint, test, and security-scan tools and triggered automatically on every task completion — so that the lead only ever integrates already-reviewed code.

[[BlogPosting/claude-code-swarms]], written when the feature entered research preview, notes that the community had been calling such coordinated teams "swarms". It describes the team being requested in natural language, with the lead spawning teammates and a mailbox for direct messaging between them. It gives the shared task list's states as pending, in progress and completed, with a pending task that has unresolved dependencies unable to be claimed until they complete, and task claiming using file locking to prevent race conditions. Teams and tasks are stored locally under `~/.claude/teams/` and `~/.claude/tasks/`. The same post describes two display modes — in-process, where all teammates run inside the main terminal (the default), and split panes via tmux or iTerm2 — as well as optional plan approval, in which a teammate works in read-only mode until the lead approves its approach, and a delegate mode that restricts the lead to coordination.

The post contrasts agent teams with subagents: subagents report results back to a single parent and cannot talk to each other, while teammates share findings, challenge each other's approaches and coordinate independently, at a higher token cost because each teammate is a separate Claude instance. It lists as limitations of the experimental feature that in-process teammates are not restored on session resumption, task status can lag, a lead manages only one team per session and teammates cannot spawn their own teams, and all teammates start with the lead's permission settings.

## Related Terms

[[SoftwareApplication/claude-code]], [[DefinedTerm/sub-agent-architecture]]
