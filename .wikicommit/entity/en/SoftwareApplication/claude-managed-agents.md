---
title: "Claude Managed Agents"
type: "schema:SoftwareApplication"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
  - type: url
    url: 'https://www.anthropic.com/engineering/managed-agents'
    hash: sha256:058bb96f68b5ec148e00110cca6d9517e4d5dcba8d1d14b840b8aef1a5da3ed2
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Anthropic's hosted service in the Claude Platform for running long-horizon agents, built around stable interfaces that decouple the session (an append-only event log), the harness that calls Claude, and the sandboxes and tools that perform actions."
  applicationCategory: "Hosted agent runtime"
  featureList: "Session, harness and sandbox as independently replaceable components; stateless harness recoverable via wake(sessionId) from an append-only session log; sandboxes provisioned on demand through a tool call; credentials kept unreachable from the code-execution sandbox; MCP tools called through a proxy backed by a credential vault"
  author: "[[Organization/anthropic]]"
---

Claude Managed Agents is [[Organization/anthropic]]'s hosted service in the Claude Platform for running long-horizon agents on a customer's behalf. Anthropic's own account of its design, [[BlogPosting/scaling-managed-agents-decoupling-the-brain-from-the-hands]], describes it as built around "a small set of interfaces meant to outlast any particular implementation", on the reasoning that agent harnesses encode assumptions about what Claude cannot do on its own and those assumptions go stale as models improve. Addy Osmani's overview of long-running agents describes it as Anthropic's hosted runtime, launched in early April.

The design follows what this wiki calls the [[DefinedTerm/brain-hands-session-split]]: Anthropic virtualizes an agent into a session (the append-only log of everything that happened), a harness (the loop that calls Claude and routes its tool calls) and a sandbox (an execution environment where Claude can run code and edit files), so that the implementation behind each can be swapped without disturbing the others. Anthropic calls the result a [[DefinedTerm/meta-harness]] — unopinionated about the specific harness Claude will need, and able to accommodate general-purpose harnesses such as [[SoftwareApplication/claude-code]] as well as task-specific ones.

## Capabilities

The harness does not live inside the sandbox; it calls a container the way it calls any other tool, through an `execute(name, input) → string` interface, and a failed container surfaces to Claude as a tool-call error, after which a new one can be provisioned from a standard recipe. The harness is itself stateless: because the session log sits outside it, a failed harness can be rebooted with `wake(sessionId)`, retrieve the event log with `getSession(id)` and resume from the last event. Anthropic describes the session as a context object that lives outside Claude's context window: `getEvents()` lets the harness select positional slices of the event stream, and any transformation of those events before they reach Claude — context engineering, prompt-cache optimization — is left to the harness.

Containers are provisioned only when a session needs one, so inference can start as soon as the orchestration layer pulls pending events from the session log. Anthropic reports that this dropped p50 time-to-first-token by roughly 60% and p95 by over 90%. For security, tokens are kept out of the sandbox where Claude's generated code runs: Git access tokens are used to clone the repository during sandbox initialization and wired into the local remote so that push and pull work without the agent handling the token, and custom tools are supported through MCP, with OAuth tokens held in a vault and calls made through a proxy that fetches the credentials. The same decoupling lets a harness connect to resources in a customer's own VPC without network peering, and lets one brain reach many execution environments — Anthropic writes that brains can even pass hands to one another.

## Adoption & Ecosystem

Osmani names it as one of three real options for a team building a hosted long-running agent product, alongside Google's Agent Platform and self-hosting a runtime on top of the Claude Agent SDK, Codex SDK, or Google's ADK. The trade-off he gives is the usual managed-versus-self-hosted one: Claude Managed Agents provides the brain/hands/session split, observability, identity, and an audit trail out of the box, while self-hosting trades that for control and the ability to assign different models to different roles.
