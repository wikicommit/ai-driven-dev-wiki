---
title: "Gemini Enterprise Agent Platform"
type: "schema:SoftwareApplication"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "Google's enterprise platform for building and running AI agents, announced at Cloud Next '26, folding Vertex AI into a single stack of named services for long-running execution, persistent memory, sandboxed execution, and fleet-level identity, policy, and observability."
  applicationCategory: "Enterprise agent platform"
  featureList: "Agent Runtime; Agent Sessions; Agent Memory Bank; Agent Sandbox; Agent-to-Agent Orchestration; Agent Registry; Agent Identity; Agent Gateway; Agent Observability; Agent Simulation"
  author: "[[Organization/google]]"
---

The Gemini Enterprise Agent Platform is Google's enterprise platform for building and running AI agents, announced at Cloud Next '26. The announcement folded Vertex AI into this single platform and turned long-running agents into a named product with named SLAs, bundled with the code-first Agent Development Kit (ADK) and the visual Agent Studio.

## Capabilities

Agent Runtime supports agents described as able to "run autonomously for days at a time," with sub-second cold starts and on-demand sandbox provisioning; the launch post's example use case is a sales-prospecting sequence that plays out over a week. Agent Sessions persist conversation and event history and can be pinned to a custom session ID that maps to an external CRM or database record, so agent state lives next to the business state it concerns. Agent Memory Bank, generally available as of Cloud Next '26, is the platform's persistent long-term memory layer: it curates memories from sessions, scopes them to a user identity, and exposes a search API so a later agent invocation can retrieve what is relevant; Payhawk reported that an expense-submission agent backed by Memory Bank cut submission time by over 50%. Agent Sandbox handles hardened code execution, and Agent-to-Agent Orchestration, Agent Registry, Agent Identity, Agent Gateway, Agent Observability, and Agent Simulation cover the fleet-level operational concerns -- including cryptographic identity and audit logging -- that a team running many agents would otherwise build by hand.

## Adoption & Ecosystem

The platform is described as architecturally the same [[DefinedTerm/brain-hands-session-split]] Anthropic set out, and as looking much like the pattern Anthropic and Cursor each separately describe, just productized at platform scale and bundled with ADK and Agent Studio rather than left for a team to assemble from scratch. It is named as one of the real managed options for a team building a hosted agent product, alongside [[SoftwareApplication/claude-managed-agents]], and as the recommended stack -- ADK plus Memory Bank plus Cloud Run plus Cloud Scheduler -- for autonomous, operational agents such as monitoring or research sweeps that accumulate state and alert on a threshold.
