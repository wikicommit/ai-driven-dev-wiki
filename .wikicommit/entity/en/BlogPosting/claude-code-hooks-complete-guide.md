---
title: "Claude Code Hooks Complete Guide - Deterministic Enforcement Across the Tool Lifecycle"
type: "schema:BlogPosting"
lang: en
tags: [agent-safety, guardrails, tool-use, agent-config]
sources:
  - type: url
    url: 'https://hidekazu-konishi.com/entry/claude_code_hooks_complete_guide.html'
    hash: sha256:66f427a7be411fa79c42761b1304353ab4194737429bda9adf85af056786ff4a
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A June 2026 reference guide by Hidekazu Konishi to hooks in Claude Code's CLI: where each hook event fires in a turn, how a hook answers through exit codes or JSON, how matchers and the settings hierarchy scope it, worked examples, and the security model and pitfalls of running hooks."
  author: ["Hidekazu Konishi"]
  datePublished: "2026-06-07"
---

This guide, published on Hidekazu Konishi's own site as the deep-dive companion to his broader guide
on Claude Code harness and environment engineering, treats [[DefinedTerm/agent-hooks]] in
[[SoftwareApplication/claude-code]] as an enforcement layer and works through it end to end. Its
premise is stated in two sentences: "A system prompt is a request. A hook is a guarantee." A hook is
a user-defined command — or HTTP endpoint, MCP tool, or sub-model evaluation — that the harness, not
the model, executes at a fixed point in the tool-and-conversation lifecycle, so enforcement becomes
deterministic where a prompt is only probabilistic.

The guide covers hooks as configured for the CLI through `settings.json` and component frontmatter,
and says that its event names, input fields, exit-code semantics and JSON fields were checked against
the official hooks reference at the time of writing, which it names as authoritative because the set
of events keeps growing. It is aimed at platform and security engineers and at developers who want
the agent to run autonomously without giving up deterministic guardrails.

## Key Points

- The guide maps hook events onto the phases of a turn — session, prompt, a tool loop that repeats per
  tool call, subagents and tasks, context compaction, the end of the turn, and display, file and MCP
  events — and counts on the order of thirty events at the time of writing, of which it says a
  handful (`PreToolUse`, `PostToolUse`, `UserPromptSubmit`, `Stop`, `SessionStart`, `SubagentStop`,
  `PreCompact`) carry most of the weight in practice.
- It describes `PreToolUse` as the strongest control surface: a `deny` from it is evaluated before any
  permission-mode check, so it blocks a tool even under `bypassPermissions`, while an `allow` only
  skips the interactive prompt and cannot override a matching `deny` or `ask` rule — a hook can
  tighten the permission system but never loosen it.
- A hook answers through two channels: the exit code, where `2` is a blocking error whose `stderr`
  becomes the reason and any other non-zero code is a non-blocking error; and a JSON object on
  standard output. Most decision-capable events use a top-level `decision: "block"`, while
  `PreToolUse` uses `hookSpecificOutput.permissionDecision` with `allow`, `deny`, `ask` or `defer`;
  the guide calls confusing the two shapes the single most common hook bug, since the wrong shape
  silently does nothing.
- Not every event blocks on exit `2`: for `PostToolUse` it only surfaces `stderr` to the model, and for
  informational events such as `SessionStart` it blocks nothing. Plain-text standard output from
  `UserPromptSubmit`, `UserPromptExpansion` and `SessionStart` is injected into the model's context,
  which the guide presents as the simplest way to add context.
- A matcher made only of letters, digits, `_` and `|` is an exact match; anything else is a
  JavaScript regular expression. The guide flags the trap this creates for MCP tools: `mcp__memory`
  never matches `mcp__memory__create_entities`, so matching a whole server needs a pattern such as
  `mcp__memory__.*`.
- Hooks from all settings layers are merged with the resolution order Managed > Local > Project >
  Plugin > User, so a hook in managed policy settings cannot be overridden by a user, and
  `allowManagedHooksOnly: true` blocks every user, project and plugin hook. Skills and subagents can
  also carry hooks in their frontmatter that are active only while the component is loaded.
- It lists five handler types — `command`, `http`, `mcp_tool`, `prompt` (a Claude model answers a
  yes/no question) and an experimental `agent` type — and gives worked examples for auto-formatting
  after writes, denying edits to secrets and destructive shell commands, asynchronous audit logging, a
  `Stop` hook that blocks the end of a turn once while there are uncommitted changes, injecting
  repository state at session start, checkpointing notes before automatic compaction, rejecting
  prompts during a deployment freeze, and rewriting a force-push into `--force-with-lease` through
  `updatedInput`.
- It distinguishes three control surfaces for one requirement: [[DefinedTerm/claude-md]] is guidance
  the model follows most of the time, permissions are a deterministic static allow/deny layer, and
  hooks are programmable enforcement that can inspect contents, call a policy service or rewrite a
  call — in its phrase, "`CLAUDE.md` persuades, permissions filter, hooks enforce-and-react", with a
  hardened setup running all three.
- Its security model starts from a hook being arbitrary code that runs automatically with the user's
  full shell privileges: hooks shipped in a cloned repository's settings should be reviewed like a
  `Makefile` or `postinstall` script, a rewriting hook becomes the author of the tool call and is the
  most safety-critical code in a hook set, an `http` hook sends hook input off the machine, and audit
  logs can contain secrets.
- Among the pitfalls it names are slow synchronous hooks on every matching tool call, a guard that
  exits `1` and so lets the action through, a `Stop` hook with no termination condition that loops
  forever, assuming subagents behave like the main agent, and over-hooking preferences whose
  occasional miss would cost little.

## Context

The guide positions itself as one article in a series by the same author covering Claude Code's
harness, settings, subagents and CI use, and limits itself to hooks for the CLI; the Claude Agent
SDK's programmatic hook interface is left to a separate article of his. It presents its regex-based
secret and command guard as defence in depth rather than a complete security boundary, since a
determined adversary can obfuscate a command past a regular expression.
