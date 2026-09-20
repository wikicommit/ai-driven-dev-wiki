---
title: "Agent2Agent Protocol (A2A)"
type: "schema:DefinedTerm"
lang: en
tags: [agents, multi-agent, agent-tooling, agent-architecture]
sources:
  - type: url
    url: 'https://www.imda.gov.sg/-/media/imda/files/about/emerging-tech-and-research/artificial-intelligence/mgf-for-agentic-ai.pdf'
    hash: sha256:ade20c2fa2aedf4f9ea3efe129e8b2ed3cc7823b414e766050586231d956645e
  - type: url
    url: 'https://www.langchain.com/blog/agentic-engineering-redefining-software-engineering'
    hash: sha256:5799c63ef9d6f2d03dd3a460a970c8adca733f9ac55a80be400ce5edb58db2fe
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A standard defining how agents communicate with each other, listed as the agent-to-agent counterpart to the Model Context Protocol's agent-to-tool role."
---

The Agent2Agent Protocol, abbreviated A2A, is a standard defining how agents communicate with each
other. It is one of the protocols — standardised ways for agents to communicate with tools and
other agents — that [[TechArticle/model-ai-governance-framework-for-agentic-ai]] lists among an
agent's core components, and it is positioned there as the agent-to-agent counterpart to
[[DefinedTerm/model-context-protocol]], which was developed for agents to communicate with tools.
That framework notes this is a fast-developing space, with more protocols being developed to
standardise agent interactions, especially in agentic commerce.

## Usage

Protocols are treated in that framework as a source of risk as well as a component: they can be
poorly deployed or compromised, the example given being an untrusted MCP server containing code to
exfiltrate a user's data. Its recommended controls for multi-agent interactions do not name A2A
specifically but bear on any agent-to-agent channel — requiring agents to communicate through
structured schemas such as typed function calls rather than free text, so as to reduce unintended
instructions passing between agents, and limiting shared memory access between agents.

A reported deployment shows what using it costs in practice.
[[BlogPosting/agentic-engineering-swarms-of-ai-agents]] describes a multi-agent engineering system
in which all worker agents communicate via A2A, while agents that do not support it are reached
through an [[DefinedTerm/model-context-protocol]] wrapper. Its authors found the AI coding agent
they wanted to integrate had no native A2A capability, and built an MCP adapter tool to route
requests from that coding agent to the worker agent — an arrangement they say makes the system
IDE-agnostic.

## Related Terms

[[DefinedTerm/model-context-protocol]], [[DefinedTerm/ai-agent]]
