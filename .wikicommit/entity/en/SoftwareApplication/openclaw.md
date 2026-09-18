---
title: "OpenClaw"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-architecture]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.05786'
    hash: sha256:88932db1701d24427b3c99749daed01d7948095ccb89ce4e1db8c125b09b160f
  - type: url
    url: 'https://arxiv.org/pdf/2604.14228'
    hash: sha256:c6ebed0a2e24b61491efe18f003cf6d6c018a671a732b3d6e331a5fe195a0e9d
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An open-source, local-first AI assistant gateway that connects messaging surfaces to an embedded agent runtime, executing tools and communicating on behalf of the developer, with a manifest-first plugin system and a structured long-term memory subsystem."
  applicationCategory: "AI agent"
  featureList: "Tool execution; messaging across WhatsApp, Telegram, Slack, Discord and Signal; manifest-first plugin system with a central registry; separate skills layer with a public registry; built-in MCP server and outbound client; structured long-term memory with optional hybrid retrieval"
  author: "Peter Steinberger and OpenClaw Contributors"
---

OpenClaw is an open-source AI agent that can execute a variety of tools and communicate openly on behalf of the developer on online platforms, with human users or with other AI agents. Its capabilities can be extended by registering a named skill, which the agent may then invoke as a tool call.

[[ScholarlyArticle/dive-into-claude-code]] describes it more specifically as a local-first WebSocket gateway that connects messaging surfaces — WhatsApp, Telegram, Slack, Discord, Signal and others — to an embedded agent runtime, with companion apps on macOS, iOS and Android, and characterizes it as a persistent control plane for multi-channel personal assistance rather than a repository-bound coding tool. It runs as a persistent daemon owning all messaging surface connections and coordinating clients, tools and device nodes over a typed WebSocket protocol.

The agent is also used as the implementation target in [[ScholarlyArticle/proof-of-guardrail-in-ai-agents]], which deploys it inside a [[DefinedTerm/trusted-execution-environment]] so that users can verify which guardrail was applied to its responses. In that reported deployment its model calls were served by external LLM APIs with GPT-5.1 as the backend model, and it was packaged for an enclave alongside a minimal Linux kernel and Node.js and Python dependencies.

## Capabilities

OpenClaw plans, invokes tools, and responds to new messages on online communication platforms. Its model access is configurable enough that it can be pointed at a single local endpoint: the [[DefinedTerm/proof-of-guardrail]] implementation launches a local proxy LLM server inside the enclave and configures it as the only available LLM option for OpenClaw, so that every input, tool call and output passes through that proxy. The same work notes that response streaming was disabled in its setup for ease of guardrail execution.

Capabilities can be registered as named skills, which the agent can then decide to invoke. Registering the enclave's attestation service as an "attestation skill" let the agent proactively offer an attestation when it received a high-stakes question, rather than only on explicit request — the paper's illustration is a user asking whether to put their savings into a newly launched token and receiving both a cautionary answer and an attestation of it.

The architectural study describes the runtime as an embedded agent core sitting inside a larger gateway dispatch layer: the gateway's agent RPC validates parameters, resolves sessions and returns immediately, while the embedded runner executes the agentic loop and emits lifecycle and stream events back through the gateway protocol. Runs are serialized through per-session queues and an optional global lane, which prevents tool and session races across the multi-channel surface.

Extension is manifest-first. Plugins register capabilities into a central registry across twelve capability types — including text inference, speech, media understanding, image, music and video generation, web search and messaging channels — and the gateway reads that registry to expose tools, channels, provider setup, hooks, HTTP routes, CLI commands and services. A separate skills layer draws from workspace, project, personal, managed, bundled and extra directories, with workspace skills taking highest precedence, alongside a public registry; MCP is supported through built-in server and outbound-client commands.

Memory is handled as its own subsystem rather than as a by-product of context management. Workspace bootstrap files are injected into the system prompt at session start, and the memory system manages long-term durable facts, date-stamped daily notes, and an optional file for background consolidation summaries. Where an embedding provider is configured, memory search combines vector similarity with keyword matching, and an experimental background process scores candidates and promotes only qualified items from short-term recall into long-term memory. Before compaction the agent is automatically reminded to save important notes to memory files.

## Safety posture

The architectural study contrasts OpenClaw's security model with per-action approval systems: it assumes a single trusted operator per gateway instance, and begins with identity and access control — direct-message pairing codes, sender allowlists and gateway authentication — rather than per-action safety classification. Tool policy uses configurable allow and deny lists per agent rather than a centralized classifier. Sandboxing is available as an opt-in feature with multiple backends and configurable scope, but is not active by default, and the project's security documentation explicitly states that hostile multi-tenant isolation on a shared gateway is not a supported security boundary.

Multi-agent behaviour is split into two separate concerns. A single gateway can host multiple fully isolated agents, each with its own workspace, authentication profiles, session store and model configuration, routed to channels or senders by deterministic binding rules. Separately, within a single agent, background runs can be spawned with configurable nesting depth and thread-bound sessions. The study notes that the project's own vision explicitly rejects agent-hierarchy frameworks as a default architecture.

## Adoption & Ecosystem

In the authors' demonstration, OpenClaw ran as an AI bot on Telegram, responding automatically to user messages, with other users in the chat able to request an attestation document at any time through a chat command. The authors characterize the agent as powerful and open-source, and exemplify their implementation with it.

The architectural study reports that OpenClaw can host [[SoftwareApplication/claude-code]], OpenAI Codex and Gemini CLI as external coding harnesses through its Agent Client Protocol integration, which it offers as evidence that gateway-level systems and task-level harnesses compose rather than compete. It is used in that paper, alongside [[SoftwareApplication/hermes-agent]], as an independent point of comparison for Claude Code's design choices.
