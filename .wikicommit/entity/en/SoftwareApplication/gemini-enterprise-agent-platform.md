---
title: "Gemini Enterprise Agent Platform"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-platforms, deployment]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
  - type: url
    url: 'https://developers.googleblog.com/agents-cli-in-agent-platform-create-to-production-in-one-cli/'
    hash: sha256:3e885a3a1f0cd7d3569bd0492c6f94334876f6d2ff073e6d5514b7c77d7deffa
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Google's enterprise platform for building and running AI agents. As reported by Addy Osmani, it folded Vertex AI into a single stack of named services for long-running execution, persistent memory, sandboxed execution, and fleet-level identity, policy and observability."
  applicationCategory: "Enterprise agent platform"
  featureList: "Agent Runtime; Agent Sessions; Agent Memory Bank; Agent Sandbox; Agent-to-Agent Orchestration; Agent Registry; Agent Identity; Agent Gateway; Agent Observability; Agent Simulation"
  author: "[[Organization/google]]"
---

The Gemini Enterprise Agent Platform is Google's enterprise platform for building and running AI agents. Writing shortly after its announcement, Addy Osmani reports that it folded Vertex AI into this single platform and turned long-running agents into a named product with named SLAs; he frames it as bundled with the code-first Agent Development Kit (ADK) and the visual Agent Studio.

## Capabilities

Osmani reports that Agent Runtime supports agents advertised as able to "run autonomously for days at a time," with sub-second cold starts and on-demand sandbox provisioning, and relays an example use case of a sales-prospecting sequence that takes a week to play out. Agent Sessions persist conversation and event history and can be pinned to a custom session ID that maps to an external CRM or database record, so agent state lives next to the business state it concerns. Agent Memory Bank, which he records as generally available, is the platform's persistent long-term memory layer: it curates memories from sessions, scopes them to a user identity, and exposes a search API so a later agent invocation can retrieve what is relevant; he relays a report from Payhawk that an expense-submission agent backed by Memory Bank cut submission time by over 50%. Agent Sandbox handles hardened code execution, and on his assessment Agent-to-Agent Orchestration, Agent Registry, Agent Identity, Agent Gateway, Agent Observability, and Agent Simulation cover basically every operational concern -- including the cryptographic identity and audit logging he says enterprises need to ship -- that a team running a production fleet would otherwise build by hand.

Google has also published a command-line interface over the same stack. [[SoftwareApplication/agents-cli]] is presented as a unified programmatic backbone for the agent development lifecycle across this platform, Cloud Run and A2A integration, covering scaffolding, evaluation, infrastructure provisioning and deployment to Agent Runtime, Cloud Run or GKE, and registering a finished agent with Gemini Enterprise for distribution. Its stated audience is notable: it is optimized for AI coding assistants to consume, while also supporting a Human Mode in which a developer runs the same commands directly. The argument given for that design is that a fragmented set of cloud components costs an assistant time and tokens in documentation before it can build anything.

## Adoption & Ecosystem

Osmani describes the platform as architecturally the same [[DefinedTerm/brain-hands-session-split]] Anthropic set out, and as looking much like the pattern Anthropic and Cursor each separately describe, just productized at platform scale and bundled with ADK and Agent Studio rather than left for a team to assemble from scratch. He names it as one of the real managed options for a team building a hosted agent product, alongside [[SoftwareApplication/claude-managed-agents]], and calls ADK plus Memory Bank plus Cloud Run plus Cloud Scheduler the cleanest stack he has seen for autonomous, operational agents such as monitoring or research sweeps that accumulate state and alert on a threshold.
