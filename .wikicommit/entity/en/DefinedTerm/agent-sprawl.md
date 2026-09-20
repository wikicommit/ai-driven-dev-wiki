---
title: "Agent Sprawl"
type: "schema:DefinedTerm"
lang: en
tags: [agents, multi-agent, governance, agent-safety]
sources:
  - type: url
    url: 'https://www.imda.gov.sg/-/media/imda/files/about/emerging-tech-and-research/artificial-intelligence/mgf-for-agentic-ai.pdf'
    hash: sha256:ade20c2fa2aedf4f9ea3efe129e8b2ed3cc7823b414e766050586231d956645e
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The uncontrolled proliferation of AI agents within an organisation without centralised management, listed as a multi-agent risk leading to provenance problems and incompatibility between agent generations."
---

Agent sprawl is the uncontrolled proliferation of AI agents within an organisation without
centralised management, as more agents are created and deployed.
[[TechArticle/model-ai-governance-framework-for-agentic-ai]] lists it first among the multi-agent
risks that the increase in the number of interacting agents brings, and names three consequences:
problems with provenance, incompatibility between old and new agents, and difficulty managing
agents from different generations that may not communicate well with each other.

## Usage

The framework's remedy sits in its treatment of agent identity rather than in a control of its own.
All agent identities and their attendant permissions should be issued from and tracked by a
centralised system, which is what lets an organisation know which agents it has deployed, spot
anomalies, and remove identities that are no longer required. That recommendation is one of four
the framework makes about an agent's identity, alongside each agent having its own unique,
cryptographically verifiable identity, that identity being tied to a supervising agent, human user
or department for accountability, and being differentiated according to the capacity in which the
agent acts.

## Related Terms

[[DefinedTerm/ai-agent]], [[DefinedTerm/sub-agent-architecture]], [[DefinedTerm/action-space]]
