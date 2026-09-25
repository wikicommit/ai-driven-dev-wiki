---
title: "Procedural Gap"
type: "schema:DefinedTerm"
lang: en
tags: [agent-skills, agent-architecture, tool-use]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.07358'
    hash: sha256:096f5ed37573599d6a6c7ead31f91dbe0c836695066c0ed2890efe4a97108983
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The shortfall between an LLM agent having access to tools and being able to use them reliably: access alone does not say when a capability should be invoked, how several should be sequenced, how failures should be handled, or how outputs should be validated."
---

The procedural gap is the name [[ScholarlyArticle/comprehensive-survey-on-agent-skills]] gives to
the distance between an LLM-based agent's access to external capabilities and robust execution of a
task with them. Access to tools — through APIs, plugins or protocol layers such as the
[[DefinedTerm/model-context-protocol]] — does not determine when a capability should be invoked, how
multiple tools should be coordinated, how failures should be handled, or how outputs should be
validated. When that orchestration is left to the model at inference time, the survey argues, it
becomes a major source of brittleness, high latency and unreliability, particularly as tasks become
long-horizon and heterogeneous.

## Usage

The survey uses the term to locate [[DefinedTerm/agent-skills]] in an agent's capability stack. It
distinguishes *passive* knowledge absorbed into a model's parameters through pre-training, fine-tuning
and alignment — static, opaque and often weak in specialized or fast-changing domains — from *active*
knowledge obtained at runtime by retrieving documents, invoking tools and APIs, accessing MCP servers
and executing skills. Active knowledge is more dynamic and grounded, but on the survey's account
access to it still does not say what should be used, when, in what sequence, or how its outputs should
be checked; that is the gap.

The survey's illustration is that a tool exposes an atomic capability — what can be done, not how it
should be used. A search tool does not say when search is preferable to memory retrieval; an API tool
does not say what to do when a schema changes; a code interpreter does not say how outputs should be
validated. It reads MCP and similar infrastructure as solving an interoperability problem rather than
this procedural one, and presents skills — reusable procedural artifacts specifying when and how
external capabilities should be applied — as what closes it.

## Related Terms

- [[DefinedTerm/agent-skills]] — what the survey proposes as the bridge across the gap
- [[DefinedTerm/tool-use-design-pattern]] — the capability access the gap sits on top of
- [[DefinedTerm/model-context-protocol]] — infrastructure the survey reads as solving interoperability, not this gap
