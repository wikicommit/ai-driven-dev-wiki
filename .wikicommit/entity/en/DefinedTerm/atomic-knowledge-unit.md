---
title: "Atomic Knowledge Unit"
type: "schema:DefinedTerm"
lang: en
tags: [agent-skills, governance, knowledge-management, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.14805'
    hash: sha256:0ff4a5fc6b09e507e775e3b0df827ae20b8cc4d5994b2fb54588b6ae501ad35b
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An AI Skill specialized for institutional knowledge delivery, proposed in Knowledge Activation: the minimal self-contained bundle of intent, procedural knowledge, tool bindings, organizational metadata, governance constraints, continuation paths and validators that lets an agent execute a single coherent action in an enterprise context."
  termCode: "AKU"
---

An Atomic Knowledge Unit (AKU) is defined in [[ScholarlyArticle/knowledge-activation]] as "an AI Skill specialized for institutional knowledge delivery" — specifically, "the minimal self-contained bundle of intent, procedural knowledge, tool bindings, organizational metadata, governance constraints, continuation paths, and validators that enables an autonomous agent to execute a single coherent action within an enterprise software development context." The paper gives *atomic* a precise sense: removing any component degrades the agent's ability to act correctly, and the unit addresses exactly one coherent action rather than a collection of loosely related tasks.

## Usage

The contrast the term is built against is retrieval. Rather than returning documents for an agent to interpret, an AKU is meant to deliver an action-ready specification — encoding what to do, which tools to use, what constraints to respect, and where to go next — so that the agent acts correctly and the engineers working alongside it receive institutionally grounded guidance without reconstructing organizational context from scratch.

Four additions specialize the [[DefinedTerm/agent-skills]] primitive into an AKU, each named against a gap its author identifies in the standard. **Governance constraints** embed permission boundaries and compliance requirements, which the paper says the standard does not address. **Continuation paths** connect otherwise isolated skills into navigable workflows, for which it says the standard has no equivalent. **Validators** — deterministic pre-execution, post-execution and invariant scripts — enforce governance programmatically, extending the standard's `scripts/` directory into a structured verification mechanism. **Organizational metadata** turns the standard's generic key-value metadata field into a specific enterprise vocabulary covering team ownership, service tier, SLA, environment classification, on-call rotation and cost centre attribution.

The unit is not meant to stand alone. Because each AKU declares its relationships to others, a corpus forms a composable knowledge graph that agents traverse at runtime, with golden paths emerging from the topology at runtime rather than being authored as separate artifacts. The analogy the paper offers for the unit's role is an instruction in a processor's instruction set architecture: a well-defined, self-contained unit that can be invoked independently and composed with others to accomplish higher-order tasks.

The gap the specialization is meant to fill is stated as an observation about practice: most AI Skills deployed in practice are general-purpose agent instructions — coding conventions, tool preferences, repository guidelines — and the paper states that the vast majority of deployed AI Skills lack the governance and security constraints that enterprise institutional knowledge delivery demands.

Evidence for the design is one enterprise deployment, of 87 skills at Yahoo, which the paper's author — who works there — presents explicitly as an existence proof supporting a structural rather than a magnitude claim.

## Related Terms

An AKU is a specialization of [[DefinedTerm/agent-skills]]; the paper places both in a lineage of earlier ad hoc mechanisms for delivering structured knowledge to agents, alongside [[DefinedTerm/agents-md]] and other repository-level [[DefinedTerm/context-files]].
