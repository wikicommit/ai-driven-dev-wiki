---
title: "Codex app-server"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-harness, coding-agents, open-source, human-oversight]
sources:
  - type: url
    url: 'https://developers.openai.com/blog/codex-as-a-platform'
    hash: sha256:f11a770f50c28f9e474cc72c15c33a9564aeb6eb21371cbaf0a6c7929f2d1b62
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An open-source OpenAI component that exposes the Codex agent harness to other applications through a documented client protocol, letting a product run Codex as its agent loop while keeping its own interface, tools and approval flow."
  applicationCategory: "Agent harness integration server"
  featureList: "Connection to a local Codex process; creating threads and starting turns; streamed events; interrupting work; exposing application tools; handling approval requests; persistent conversations"
  author: "[[Organization/openai]]"
---

Codex app-server is the component through which OpenAI exposes the Codex agent harness — the system that powers the Codex app, CLI and IDE extension of [[SoftwareApplication/openai-codex]] — to other applications. According to [[BlogPosting/codex-as-a-platform]], it offers the harness's capabilities through a documented client protocol: applications can create threads, start turns, receive events and handle approval requests. OpenAI publishes it as open source, alongside the Codex CLI and the official Codex SDK.

OpenAI's pitch for it is that a team building software that needs an agent can start with Codex instead of inventing a new runtime, and then decide what the surrounding application should own.

## Capabilities

The post describes app-server as letting an application connect to a local Codex process, keep conversations open, stream events, interrupt work, expose tools and respond to approval requests. Underneath, the Codex harness manages conversation state, streams execution, uses tools, enforces configured sandbox and approval policies, and carries work across turns.

OpenAI positions it as one of three ways to build on Codex: `codex exec` for bounded non-interactive jobs such as a script or CI task, the Codex SDK for programmatic workflows that start, resume or stream tasks, and app-server "when the agent is part of the product itself". In the post's words, the SDK simplifies common programmatic workflows, while app-server gives product teams direct control over the lifecycle and user experience.

## Adoption & Ecosystem

The division of labour OpenAI describes is that the application owns product context, business rules, tools and consent, while app-server provides the agent loop and sandboxed execution. Its worked example is Relay, a sample operations application OpenAI built on app-server: an agent sits beside a fictional shipment dashboard, connected to application-owned MCP tools ([[DefinedTerm/model-context-protocol]]), and must obtain human approval before rebooking a shipment. The harness handles the agent loop, conversation state, streamed activity and tool interaction, while the product keeps its dashboard, records and controls.
