---
title: "Claude Managed Agents"
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
  description: "Anthropic's hosted runtime for long-running AI agents, launched in early April, built around a Brain/Hands/Session architecture that separates the model-and-harness loop from sandboxed execution and from a durable, append-only session log."
  applicationCategory: "Hosted agent runtime"
  featureList: "Brain/Hands/Session split; stateless harness; ephemeral sandboxes; session recovery via wake(sessionId) against an append-only event log; credentials kept unreachable from the code-execution sandbox"
  author: "[[Organization/anthropic]]"
---

Claude Managed Agents is Anthropic's hosted runtime for long-running AI agents, launched in early April. It is built on the architecture described in Anthropic's "Scaling Managed Agents: Decoupling the brain from the hands" post: a [[DefinedTerm/brain-hands-session-split]] that separates the model-and-harness loop (the Brain), sandboxed and ephemeral tool-execution environments (the Hands), and an append-only event log of every thought, tool call, and observation (the Session) into independently replaceable pieces.

## Capabilities

Decoupling the three components makes the harness stateless and sandboxes disposable -- "cattle, not pets" -- so a crash in the model-serving component does not lose the run: a fresh container calls `wake(sessionId)` and reconstitutes state from the session's event log rather than from a snapshot inside a single process. Anthropic reported that this dropped time-to-first-token by roughly 60% at p50 and over 90% at p95, attributed to being able to start inference before the sandbox is ready. The separation is also described as a security benefit: credentials are kept unreachable from the sandbox in which model-generated code actually runs.

## Adoption & Ecosystem

It is named as one of three real options for a team building a hosted long-running agent product today, alongside Google's Agent Platform and self-hosting a runtime on top of the Claude Agent SDK, Codex SDK, or Google's ADK. The trade-off given is the usual managed-versus-self-hosted one: Claude Managed Agents provides the brain/hands/session split, observability, identity, and an audit trail out of the box, while self-hosting trades that for control and the ability to assign different models to different roles.
