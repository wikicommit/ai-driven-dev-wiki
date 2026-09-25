---
title: "Omnigent"
type: "schema:SoftwareApplication"
lang: en
tags: [harness-engineering, orchestration, multi-agent, open-source]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2609.00006'
    hash: sha256:b2b6be03cc43e6f9b52518921f9545373563aec224327e1bb29a30beea7b7ce0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An open-source orchestration layer from Databricks that wraps whole coding-agent harnesses such as Claude Code, Codex, Cursor, OpenCode, Hermes and Pi behind a common API, adding cross-harness policies, a uniform OS sandbox and shareable multi-device sessions."
  applicationCategory: "Meta-harness (orchestration layer over coding-agent harnesses)"
  softwareVersion: "0.4.0"
  featureList: "Registry of canonical harness adapters with five integration modes (sdk-in-process, cli-subprocess, acp-subprocess, native-tui, native-server); a conformance bench probing declared adapter capabilities; any registered harness addressable as a sub-agent session of another; a three-level cross-harness policy plane with CEL, Python or LLM-classifier evaluators; a uniform sandbox and default-deny egress proxy with a secretless credential proxy; server-durable, shareable sessions with mid-session harness switching"
  author: "Databricks"
---

Omnigent is an open-source orchestration layer that Databricks released in June 2026 under the Apache 2.0
licence. [[ScholarlyArticle/harness-engineering-anatomy-architecture-and-evolution-of-coding-agents]],
which examines its source at version 0.4.0, describes it as the first [[DefinedTerm/meta-harness]] the
authors are aware of: rather than implementing an agent loop of its own, it treats entire coding-agent
harnesses — [[SoftwareApplication/claude-code]], [[SoftwareApplication/openai-codex]],
[[SoftwareApplication/cursor]], [[SoftwareApplication/opencode]], [[SoftwareApplication/hermes-agent]],
Pi and custom YAML-defined agents among them — as interchangeable components behind a common API.

The paper reads it as a bet that the [[DefinedTerm/agent-harness]] has become a commodity component and
that durable value sits one layer up, and uses it as a contrast point rather than as a corpus member: it
implements no editing loop, no repository context and no edit-application strategy, so the authors
decline to score it on the same subsystems as the harnesses they study.

## Capabilities

On the paper's account Omnigent runs as a four-tier process topology — server, host daemon, runner, and a
per-conversation harness subprocess — whose adapter boundary is, by design, a recursive subset of its own
public REST API. Its registry ships 23 canonical harness adapters plus aliases and a community
entry-point group, formalized into five integration modes, and declared adapter capabilities are
reconciled against a conformance bench that probes basic turns, tool calling, streaming, interrupts, model
override and policy denial; the paper reports live verification for the four flagship SDK adapters and
best-effort declarations for the rest.

Above that boundary the paper identifies four additions: composition, so that a Claude-brained
orchestrator can dispatch work to Codex and have Cursor review it; a cross-harness policy plane with
session, agent and admin levels, enforced on foreign harnesses through each vendor's own extension
mechanism such as Claude Code hooks, Cursor hooks, Hermes hooks and ACP permission requests, with
fail-closed semantics; a uniform sandbox — bubblewrap plus seccomp on Linux, generated Seatbelt profiles
on macOS and Job Objects on Windows — with a default-deny egress proxy hosting a credential proxy that
keeps real tokens out of the sandbox; and server-durable sessions with multi-device sync, access grants,
review comments, forking and mid-session harness switching.

The paper also notes what Omnigent does not do. Vendor-specific capability records and endpoints leak
through its common API by design, and sandboxing is applied inconsistently — it wraps the Claude CLI in
its own sandbox but delegates to Codex's native sandbox modes — which the authors take as evidence that
OS-level isolation resists being factored out as a shared service. Its two baseline dependencies are
reported to be the claude-agent-sdk and openai-agents packages, which the paper uses to argue that harness
SDKs have become the framework layer for a 2026 orchestration system.

## Adoption & Ecosystem

The flagship example the paper describes, Polly, is a cross-vendor coordinator-worker setup: a Claude
Code-brained orchestrator that writes no code itself, fans work out to six vendor harnesses in per-task
git worktrees, and mandates in its prompt that the reviewer of a change come from a different vendor than
its implementer. The paper uses Omnigent as evidence for its thesis that coding harnesses have turned into
platforms, and lists the economics of such a layer — whether commoditization from above captures value
durably — as an open question.
