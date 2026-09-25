---
title: "Scaling Managed Agents: Decoupling the brain from the hands"
type: "schema:BlogPosting"
lang: en
tags: [agent-architecture, harness-engineering, long-running-agents]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/managed-agents'
    hash: sha256:058bb96f68b5ec148e00110cca6d9517e4d5dcba8d1d14b840b8aef1a5da3ed2
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An Anthropic engineering post explaining the design of Claude Managed Agents, which separates an agent's session log, harness and sandboxes behind stable interfaces so that each can fail or be replaced independently as harnesses evolve."
  author: ["Lance Martin", "Gabe Cemaj", "Michael Cohen"]
  datePublished: "2026-04-08"
  publisher: "[[Organization/anthropic]]"
---

The post explains how [[Organization/anthropic]] designed [[SoftwareApplication/claude-managed-agents]], its hosted service for long-horizon agent work. Its starting point is that agent harnesses encode assumptions about what Claude cannot do on its own, and that those assumptions go stale as models improve — its example being context resets added to a harness to counter [[DefinedTerm/context-anxiety]] in one model that became dead weight in a later one. Rather than fixing on one harness, Anthropic set out to build a system for "programs as yet unthought of," borrowing the approach operating systems took when they virtualized hardware into abstractions general enough to outlast it.

The design it describes — the [[DefinedTerm/brain-hands-session-split]] — virtualizes an agent into a session (an append-only log of everything that happened), a harness (the loop that calls Claude and routes its tool calls) and a sandbox (where Claude runs code and edits files), each behind an interface that makes few assumptions about the others. The post closes by calling Managed Agents a [[DefinedTerm/meta-harness]]: opinionated about the interfaces around Claude, unopinionated about the specific harness that runs on them.

## Key Points

- Anthropic first ran the session, harness and sandbox in one container, which made the container a "pet": its failure lost the session, and debugging it meant opening a shell in a container that often held user data.
- Moving the harness out of the container turned the container into "cattle": the harness calls it like any other tool through `execute(name, input) → string`, a dead container comes back to Claude as a tool-call error, and a new one can be provisioned with `provision({resources})`.
- The harness is stateless as well: because the session log lives outside it, a failed harness can be rebooted with `wake(sessionId)`, read back the log with `getSession(id)` and resume from the last event, writing to the session with `emitEvent(id, event)` as it goes.
- In the coupled design, code Claude generated ran alongside credentials, so a prompt injection only had to convince Claude to read its own environment. The post's structural fix is that tokens are never reachable from the sandbox: Git tokens are used to clone the repository at sandbox initialization and wired into the local remote, and MCP tools are called through a proxy that fetches OAuth credentials from a vault, so the harness is never made aware of any credentials.
- The session is not Claude's context window. Compaction, memory files and context trimming each make irreversible decisions about what to keep; the session instead durably stores every event and lets the harness select positional slices of it with `getEvents()`, leaving context engineering to the harness.
- Provisioning containers only when a session needs one means inference can start as soon as pending events are pulled from the log; Anthropic reports that this cut p50 time-to-first-token by roughly 60% and p95 by over 90%.
- The same decoupling lets a harness reach resources in a customer's own VPC without network peering, lets many stateless brains be started, and lets one brain use many hands — the post notes the harness does not know whether a sandbox is a container, a phone or a Pokémon emulator, and that brains can pass hands to one another.
- Anthropic writes that it started with a single container because earlier models could not reason about several execution environments, and that as intelligence scaled the single container became the limitation.

## Context

This is Anthropic's own account of the architecture of its own product, and its performance figures describe that service. It places itself in a running series on the Anthropic Engineering Blog about building effective agents and designing harnesses for long-running work, and it states its central bet explicitly: because the context engineering future models will need cannot be predicted, the interfaces guarantee only that the session is durable and available for interrogation and push context management into whatever harness runs on top. It gives [[SoftwareApplication/claude-code]] as an example of a general-purpose harness the system can accommodate, alongside task-specific harnesses.
