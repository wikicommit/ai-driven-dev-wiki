---
title: "Antigravity SDK"
type: "schema:SoftwareApplication"
lang: en
sources:
  - type: url
    url: 'https://antigravity.google/changelog'
    hash: sha256:b0b3bf8a83113a1801fca60c849755cf0a8bf727c40a344c5d00a49916f1a79c
  - type: url
    url: 'https://codelabs.developers.google.com/agy-cli-sdk-code-review'
    hash: sha256:283b349fe5d611bf6d0c0d2b5ac36978aaa667fac020078c52e2bf0412ba54ae
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
tags: [agents, coding-tools, agent-architecture, local-models, code-review]

properties:
  description: "The Python SDK of the Google Antigravity product family, for building and running Antigravity agents programmatically, including against local models."
  applicationCategory: "Agent development SDK"
  featureList: "Agent configuration objects; lifecycle hooks; allow/deny/ask-user safety policies; MCP server integration; subagents; built-in tools such as web search, URL fetching, command execution and scheduling; local models through LiteRT and OpenAI-compatible endpoints; budget and context-compaction controls; OpenTelemetry tracing"
  author: "[[Organization/google]]"
---

The Antigravity SDK is the Python software development kit of the
[[SoftwareApplication/google-antigravity]] product family, published under the
`google.antigravity` package. Where the desktop app, IDE and
[[SoftwareApplication/antigravity-cli]] put an agent in front of a developer, the SDK lets
a developer configure and run Antigravity agents from their own Python code. The product
changelog lists releases from 0.1.1 (May 29, 2026) to 0.1.18 (September 21, 2026).

Agents run through a local harness process that the Python client connects to; the
changelog refers to it as the `localharness` binary. Configuration is expressed as
objects such as `AgentConfig` and `LocalAgentConfig`, and much of the release history
consists of moving settings into such objects — models, retries, budgets, command
execution and context compaction.

## Capabilities

**Control over the agent loop.** Lifecycle hooks fire around sessions, turns, tool calls
and context compaction; from 0.1.13 a pre-tool hook can rewrite a tool's arguments before
it runs. Safety policies (`policy.allow`, `policy.deny`, `policy.ask_user`) decide which
tool calls proceed, and can be pointed directly at an MCP server configuration. From
0.1.11 the SDK's default `AgentBehavior` is autonomous rather than interactive, to suit
scripted, background and headless use, and from 0.1.18 the interactive `ASK_QUESTION`
tool is left out of the default toolset.

**Tools and delegation.** Agents can use [[DefinedTerm/model-context-protocol]] servers
(stdio and streamable HTTP; the older SSE transport was removed in 0.1.2), built-in web
search (0.1.4) and URL fetching (0.1.6), command execution — optionally inside an OS-level
sandbox via `RunCommandConfig(enable_sandbox=True)` (0.1.16) — and a `schedule` tool for
timers and cron-style background jobs, enabled by default from 0.1.18. Subagents can be
declared statically (0.1.5), given their own instructions and tool allowlists (0.1.8),
their own custom tools (0.1.15) and, from 0.1.18, their own model.

**Local models.** From 0.1.6 the SDK can run agents against local models:
`LiteRTAgentConfig` for Gemma models through LiteRT-LM, and `LocalOpenAIAgentConfig` for
OpenAI-compatible endpoints such as Ollama and LM Studio. 0.1.7 extended MCP and subagent
support to these backends, a `.lightweight()` preset for small local models followed in
0.1.16, and 0.1.18 announced local model support as official.

**Operational controls.** `BudgetConfig` (0.1.11) caps a session's tokens, turns and cost,
and a `StopReason` reports why a turn ended; `CompactionConfig` (0.1.17) sets the token
threshold at which conversation history is compacted; OpenTelemetry tracing (0.1.5) maps
session, turn, step and tool events to spans. 0.1.18 adds an evaluation preset,
`AgentConfig.eval()`, which the changelog describes as a standardized, benchmark-ready
configuration for core coding evaluations.

## Adoption & Ecosystem

The SDK authenticates against the Gemini Developer API or Vertex AI, including Vertex AI
Express mode with an API key, and can route through custom base URLs and enterprise
gateways. Its default model has tracked Google's Gemini Flash releases —
`gemini-3.6-flash` from 0.1.8, `gemini-3.7-flash` from 0.1.11 and `gemini-3.8-flash` from
0.1.16. Windows support was added in 0.1.2, and musllinux wheels for Alpine Linux in 0.1.15.

A Google Codelabs tutorial ([[HowTo/ai-assisted-code-review-with-antigravity-cli-and-sdk]])
shows the SDK used headless in CI. It describes the SDK, installed as the `google-antigravity`
package, as providing the same agent runtime as the Antigravity CLI as a Python library, and
states that it is currently available only in Python. The tutorial pins version 0.1.7 and builds a
read-only code-review agent from a `LocalAgentConfig`: `policy.deny_all()` followed by
`policy.allow` for file-reading tools, command execution and `finish`; a `pre_tool_call_decide`
hook that rejects any command not starting with `git`, which the tutorial presents as a second layer
of enforcement on top of the policies; a `post_tool_call` hook that logs tool results; agent skills
loaded through `skills_paths` — the same skill files the CLI loads from `.agents/skills/`, through a
different loading mechanism; and a Pydantic `response_schema` that makes the agent return structured
findings. It authenticates with a `GEMINI_API_KEY` when one is set and otherwise falls back to
Vertex AI through Application Default Credentials. The agent is then run by a GitHub Actions workflow
on each pull request, and its findings are posted as a comment.
