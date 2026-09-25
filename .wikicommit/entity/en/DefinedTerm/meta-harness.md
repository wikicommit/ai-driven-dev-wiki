---
title: "Meta-Harness"
type: "schema:DefinedTerm"
lang: en
tags: [harness-engineering, agent-architecture, multi-agent, orchestration]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2609.00006'
    hash: sha256:b2b6be03cc43e6f9b52518921f9545373563aec224327e1bb29a30beea7b7ce0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An orchestration layer that sits above coding-agent harnesses and treats whole harnesses as interchangeable components behind a common API, coordinating them from outside while implementing no editing loop of its own."
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

The term and its analysis rest on a single system and a single source-code study; the paper calls
Omnigent the first meta-harness it is aware of rather than a representative of an established category.

## Related Terms

- [[DefinedTerm/agent-harness]]
- [[DefinedTerm/harness-engineering]]
- [[DefinedTerm/system-harness]]
- [[DefinedTerm/harness-as-a-service]]
- [[DefinedTerm/multi-model-orchestration]]
