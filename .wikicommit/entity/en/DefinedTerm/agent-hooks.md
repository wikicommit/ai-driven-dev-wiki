---
title: "Agent Hooks"
type: "schema:DefinedTerm"
lang: en
tags: [agents, agent-safety, tool-use]
sources:
  - type: url
    url: 'https://ai.google.dev/gemini-api/docs/agent-hooks'
    hash: sha256:f79707693b6ab1cdff0b59d925597d980c9bf9c441da28a1505c1a9f80407641
  - type: url
    url: 'https://dev.to/aws/ai-agent-guardrails-rules-that-llms-cannot-bypass-596d'
    hash: sha256:d321340a9dfb2556bc45605cd43311d6f886dd3c139f618c6380e18345aa7a1a
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A mechanism that lets a developer run custom logic — an external script, an HTTP callback, or an in-process framework callback — immediately before or after an AI agent executes a tool call, so the call can be approved, blocked, or followed up on."
---

Agent hooks let a developer intercept an AI agent's tool calls, running custom logic right before or right after a call executes so that the call can be approved, blocked, or followed up on. The mechanism appears both as external configuration a runtime reads and as an in-process callback API an agent framework exposes; Google's Gemini API implements the first as a `hooks.json` configuration that groups event definitions under named rules, matched against tool names using standard RE2 regular expressions, while [[SoftwareApplication/strands-agents]] implements the second as callbacks registered against framework lifecycle events.

## Usage

A hook fires on one of two lifecycle events: `pre_tool_execution`, which runs before a tool call and can approve (`allow`) or block (`deny`) it before it runs — when blocked, the model sees the rejection reason and can adapt — or `post_tool_execution`, which runs after a call completes and can only perform follow-up work such as formatting code, running tests, or logging telemetry, since it cannot undo or block an action that already happened. Each rule group names a `matcher` (a regular expression matched against tool names such as `code_execution`, `read_file`, or `write_file`) and an ordered list of `hooks` to run when it matches; a hook is either a `command` (runs inside the sandbox, reading the event as JSON on stdin and writing its decision to stdout) or an `http` handler (posts the event to an external HTTPS endpoint through the sandbox's egress proxy, which can inject authentication headers on outgoing requests so secrets never need to be stored in the hook configuration itself). If a command script crashes, an HTTP hook returns a non-2xx status, or a hook times out or returns unrecognized output, the runtime treats it as an approval rather than blocking the call, so a broken hook never deadlocks the agent. In Gemini API's implementation, hooks are scoped to the sandbox's own built-in tools (code execution and filesystem operations) and do not fire for custom function-calling tools or external MCP-server tools handled outside the container.

The same pre-execution interception appears as an in-process API in [[SoftwareApplication/strands-agents]], where a `HookProvider` registers a callback against `BeforeToolCallEvent` through a `HookRegistry`. The callback receives the pending call's name and input and blocks it by assigning a message to `event.cancel_tool`, which the framework returns to the model in place of the tool's result. What the post describing it draws from that arrangement is an argument about where enforcement belongs: because the callback runs outside the model, a rule evaluated there is not something the model can reinterpret, unlike the same rule written into a prompt or a tool docstring. That use is developed under [[DefinedTerm/neurosymbolic-validation]].

The two implementations differ in what they cover and how they behave when something goes wrong, so neither description generalizes to the other. Gemini API's hooks are scoped to its sandbox's built-in tools and fail open — a crashed script, a non-2xx HTTP response, a timeout or unrecognized output is treated as an approval, so a broken hook never deadlocks the agent — whereas the Strands example intercepts the agent's own decorated tools, and the source describing it addresses only the deliberate cancellation path rather than what happens if a callback itself fails.

## Related Terms

[[DefinedTerm/sandboxing]], [[DefinedTerm/guardrails]], [[DefinedTerm/neurosymbolic-validation]], [[DefinedTerm/tool-use-design-pattern]], [[SoftwareApplication/strands-agents]]
