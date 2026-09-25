---
title: "Forked Subagent"
type: "schema:DefinedTerm"
lang: en
tags: [multi-agent, context-engineering, anthropic]
sources:
  - type: url
    url: 'https://docs.anthropic.com/en/docs/claude-code/sub-agents'
    hash: sha256:3dc673c4c846bf18c02306e373bd9485b76c7020852d44c16f0d0fb555344f0c
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "In Claude Code, a subagent that inherits the entire conversation so far — system prompt, tools, model and message history — instead of starting from a fresh context, while still returning only its final result to the main conversation."
---

A forked subagent, or fork, is a [[SoftwareApplication/claude-code]] subagent that inherits the whole
conversation so far instead of starting fresh. Anthropic's documentation contrasts it with every other
subagent, which starts from a fresh, isolated context window containing only its own system prompt, a
delegation message Claude writes, and a few loaded files: a fork instead sees the same system prompt,
tools, model and message history as the main session, which the documentation describes as dropping the
input isolation subagents otherwise provide. What it keeps is the output side of that isolation — the
fork's own tool calls stay out of the main conversation and only its final result comes back, so the
main context window stays clean.

## Usage

The documentation's stated reason for a fork is to hand off a side task without re-explaining the
situation: it recommends one when any other subagent would need too much background to be useful, or
to try several approaches in parallel from the same starting point. A user can start one with
`/subtask` followed by a task (the command was `/fork` on earlier versions); it runs in the background
in a panel below the prompt, where its transcript can be opened and sent follow-up messages, and its
result arrives as a message in the main conversation when it finishes. Claude can also start one by
requesting the `fork` subagent type through its Agent tool, which a setting called fork mode governs —
on by default in interactive sessions and off by default in non-interactive mode and the Agent SDK,
with an environment variable to override either default.

The documented differences from a non-fork subagent are that a fork uses the main session's system
prompt, tools and model rather than a definition file's, surfaces its permission prompts in the
terminal, and shares the main session's prompt cache. Because a fork's system prompt
and tool definitions are identical to the parent's, its first request reuses the parent's prompt
cache, which the documentation says makes forking cheaper than spawning a fresh subagent for tasks
that need the same context. A fork receives the main conversation's exact tool pool rather than the
filtered set other subagents get, can be given its own git worktree so its file edits do not land in
the user's checkout, and cannot spawn further forks. Unlike a non-fork subagent, whose own system prompt means the
user's output style does not shape its responses, a fork is shaped by it.

## Related Terms

- [[DefinedTerm/sub-agent-architecture]] — the broader pattern of delegating to subagents with clean
  context windows, of which a fork is the exception on the input side
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/token-caching]]
- [[DefinedTerm/git-worktrees]]
