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
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/agent/multi-agent/'
    hash: sha256:644e8c22de6fd778cefa3c3c44647eee3beb025a3fb81617e0411c473018e2c9
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A standard defining how agents communicate with each other, listed as the agent-to-agent counterpart to the Model Context Protocol's agent-to-tool role. A further source describes it as Google-led and reports a 2026 update introducing an agent directory."
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

A third source reports where the protocol has got to and names what it is being paired with. A
chapter of Jimmy Song's online handbook 智能体构建指南 describes A2A as Google-led and states that a
2026 update introduced an agent directory, which it presents as making agent discovery and invocation
across organisations and across frameworks possible. It also reports that a mainstream Python agent
framework was the first to gain native A2A support. That chapter names release dates and a version number
for both of those events in passing; they are not restated here, because the announcements behind
them are not among this page's sources.

The framing that chapter puts on the result is a two-protocol stack it says the industry is settling
into: **MCP connects tools, A2A connects agents** — the first answering how an agent reaches an
external capability, the second how agents interoperate with one another, and the two together
forming the protocol base of a [[DefinedTerm/llm-based-multi-agent-system]]. In its 2026 summary
table it lists MCP as having become the de facto standard and A2A as Google-led, with the agent
directory as its distinguishing addition. Those are stated there as assessments of where the
ecosystem stands, not as measured findings.

## Related Terms

[[DefinedTerm/model-context-protocol]], [[DefinedTerm/ai-agent]]
