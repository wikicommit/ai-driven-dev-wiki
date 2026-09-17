---
title: "Agent Hooks"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://ai.google.dev/gemini-api/docs/agent-hooks'
    hash: sha256:f79707693b6ab1cdff0b59d925597d980c9bf9c441da28a1505c1a9f80407641
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A mechanism that lets a developer run a custom script or HTTP callback immediately before or after an AI agent executes a tool call inside its sandbox, so the call can be approved, blocked, or followed up on."
---

Agent hooks let a developer intercept an AI agent's tool calls inside its execution sandbox, running a custom command or an external HTTP request right before or right after a call executes. Google's Gemini API implements this as a `hooks.json` configuration that groups event definitions under named rules, matched against tool names using standard RE2 regular expressions.

## Usage

A hook fires on one of two lifecycle events: `pre_tool_execution`, which runs before a tool call and can approve (`allow`) or block (`deny`) it before it runs — when blocked, the model sees the rejection reason and can adapt — or `post_tool_execution`, which runs after a call completes and can only perform follow-up work such as formatting code, running tests, or logging telemetry, since it cannot undo or block an action that already happened. Each rule group names a `matcher` (a regular expression matched against tool names such as `code_execution`, `read_file`, or `write_file`) and an ordered list of `hooks` to run when it matches; a hook is either a `command` (runs inside the sandbox, reading the event as JSON on stdin and writing its decision to stdout) or an `http` handler (posts the event to an external HTTPS endpoint through the sandbox's egress proxy, which can inject authentication headers on outgoing requests so secrets never need to be stored in the hook configuration itself). If a command script crashes, an HTTP hook returns a non-2xx status, or a hook times out or returns unrecognized output, the runtime treats it as an approval rather than blocking the call, so a broken hook never deadlocks the agent. In Gemini API's implementation, hooks are scoped to the sandbox's own built-in tools (code execution and filesystem operations) and do not fire for custom function-calling tools or external MCP-server tools handled outside the container.

## Related Terms

[[DefinedTerm/sandboxing]], [[DefinedTerm/guardrails]], [[DefinedTerm/tool-use]]
