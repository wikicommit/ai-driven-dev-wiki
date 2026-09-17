---
title: "Brain/Hands/Session Split"
type: "schema:DefinedTerm"
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
  description: "An architectural pattern that decouples an AI agent into three independently replaceable components: the Brain (the model and the harness loop that calls it), the Hands (sandboxed, ephemeral environments where tools actually run), and the Session (an append-only event log of every thought, tool call, and observation)."
---

The Brain/Hands/Session split is a pattern, set out by Anthropic in its "Scaling Managed Agents: Decoupling the brain from the hands" post, for building a long-running AI agent by separating it into three components that can each be replaced independently. The Brain is the model plus the harness loop that calls it. The Hands are sandboxed, ephemeral execution environments where tools actually run. The Session is an append-only event log recording every thought, tool call, and observation.

## Usage

The pattern is the architectural idea behind [[SoftwareApplication/claude-managed-agents]]. Anthropic's framing is that "every component in a harness encodes an assumption about what the model can't do on its own" -- when the three components are coupled, an assumption going stale (for example, a model that used to need an explicit planner and now plans natively) forces the whole system to change at once. Decoupling them makes the harness stateless, turns sandboxes into "cattle, not pets," and means a brain crash does not lose the run: a fresh container calls `wake(sessionId)` and reconstitutes state from the event log. Anthropic reported that this dropped time-to-first-token by roughly 60% at p50 and over 90% at p95, from being able to start inference before the sandbox is ready.

Google's Gemini Enterprise Agent Platform is described as architecturally the same brain/hands/session split, just productized at platform scale and bundled with a development kit rather than assembled by a team from scratch (see [[SoftwareApplication/gemini-enterprise-agent-platform]]).

## When It Applies

The pattern applies when building or hosting an agent expected to run for a long time, since a stateless harness and a durable event log are what make a long run recoverable rather than fragile to a container failure. Without the session-as-event-log piece, a container failure is a session failure and debugging falls back to a stale snapshot; with it, the agent's memory becomes a queryable artifact independent of whatever process happens to be running. It also matters for security: keeping credentials unreachable from the sandbox where model-generated code runs is one benefit Anthropic attributes to this separation for Managed Agents.

## Related Terms

[[DefinedTerm/long-running-agent]], [[SoftwareApplication/claude-managed-agents]], [[SoftwareApplication/gemini-enterprise-agent-platform]], [[Organization/anthropic]]
