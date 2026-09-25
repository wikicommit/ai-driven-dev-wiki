---
title: "Meta-Harness"
type: "schema:DefinedTerm"
lang: en
tags: [harness-engineering, agent-architecture, multi-agent, orchestration]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2609.00006'
    hash: sha256:b2b6be03cc43e6f9b52518921f9545373563aec224327e1bb29a30beea7b7ce0
  - type: url
    url: 'https://www.anthropic.com/engineering/managed-agents'
    hash: sha256:058bb96f68b5ec148e00110cca6d9517e4d5dcba8d1d14b840b8aef1a5da3ed2
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A layer defined relative to agent harnesses rather than as one. In one research usage it is an orchestration layer that treats whole coding-agent harnesses as interchangeable components behind a common API; Anthropic uses the term for a hosted system that stays unopinionated about which harness runs on its stable interfaces."
---

A meta-harness, in the usage of
[[ScholarlyArticle/harness-engineering-anatomy-architecture-and-evolution-of-coding-agents]], is an
orchestration layer that coordinates one or more coding-agent harnesses from above and implements no
editing loop of its own. Where an [[DefinedTerm/agent-harness]] wraps a model to make it act on a
repository, a meta-harness wraps entire harnesses — Claude Code, Codex, Cursor and others — as
interchangeable components behind a common interface. The paper treats it as one of four things a harness
is not, and scoring it on the same subsystems as a harness would, in its words, be a category error; it
analyses the first such system it is aware of, [[SoftwareApplication/omnigent]], as evidence about which
harness capabilities are migrating up into a separate layer.

## Usage

The paper describes what the meta-layer adds above the harness boundary in Omnigent's case: composition,
so that any registered harness can be addressed as a sub-agent session of any other; a cross-harness
policy plane enforced on foreign harnesses through each vendor's own extension mechanism, such as Claude
Code hooks or ACP permission requests; a uniform sandbox and egress stack; and shareable, server-durable
sessions that can switch harness mid-session. What stays below the line is the harness core — the editing
loop, repository context and edit-application strategy.

The authors read the meta-harness as a bet that the harness is becoming a commodity component and that
durable value sits one layer up, and they place it within their broader thesis that coding harnesses have
turned from tools into platforms. They note two tensions in that reading from the one system they
examine: the meta-layer does not pretend the harnesses are equivalent, with vendor-specific capability
records leaking through its common API by design, and it applies sandboxing inconsistently — wrapping one
vendor's CLI in its own sandbox while delegating to another's native sandbox modes — which the paper
takes as evidence that OS-level isolation resists being factored out as a shared service. It lists the
economics of commoditization from above as an open question for future work.

The paper's analysis rests on a single system and a single source-code study; it calls Omnigent the
first meta-harness it is aware of rather than a representative of an established category.

Anthropic uses the same word for a different design. In
[[BlogPosting/scaling-managed-agents-decoupling-the-brain-from-the-hands]] it calls
[[SoftwareApplication/claude-managed-agents]] "a meta-harness", meaning a system that is unopinionated
about the specific harness Claude will need in future and instead offers general interfaces — a durable
session and sandboxes reached through a tool-call interface — that many different harnesses can run on,
from a general-purpose one such as Claude Code to task-specific ones. Where the paper's meta-harness
coordinates existing vendors' harnesses from above, Anthropic's hosts whatever harness sits between
Claude and those interfaces, and it describes the design as being opinionated about the interfaces around
Claude rather than about the harness itself (see [[DefinedTerm/brain-hands-session-split]]). Neither
source refers to the other's usage.

## Related Terms

- [[DefinedTerm/agent-harness]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/system-harness]]
- [[DefinedTerm/harness-as-a-service]]
- [[DefinedTerm/multi-model-orchestration]]
- [[DefinedTerm/brain-hands-session-split]]
