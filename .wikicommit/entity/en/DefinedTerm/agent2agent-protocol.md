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
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-native-whitepaper/03-development-frameworks/'
    hash: sha256:387bad42083bfa6f2ac79781096a48796e1b0e141792328d9810971e043c1a93
  - type: url
    url: 'https://developers.googleblog.com/developers-guide-to-ai-agent-protocols/'
    hash: sha256:7b380e1b02a7431f86ce85fd5ad5a49d2707ee157205f5584f28284782319fef
  - type: url
    url: 'https://arxiv.org/abs/2505.02279'
    hash: sha256:7697852f9428f817d9c744137c1cc2162cddc7fa5d0876349a9b513835cce643
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A standard defining how agents communicate with each other, listed as the agent-to-agent counterpart to the Model Context Protocol's agent-to-tool role. A further source describes it as Google-led and reports a 2026 update introducing an agent directory; Google's developer guide to agent protocols presents it as the standard for how agents discover and communicate with each other, with each agent publishing an Agent Card at a well-known URL."
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

A fourth source describes the protocol's moving parts rather than its place in the ecosystem. Chapter 3
of the AI 原生应用架构白皮书 (AI-native application architecture whitepaper) hosted on jimmysong.io calls
A2A an open standard for efficient communication and collaboration between heterogeneous agents, with
three core roles — the user, the A2A client and the A2A server — and five main elements: the **Agent
Card**, JSON-format metadata describing an agent's capabilities and service endpoint; the **Task**, a
stateful unit that supports multi-turn interaction; the **Message**, the basic unit of a single
exchange; the **Artifact**, the concrete result produced once a task is complete; and the **Part**, the
smallest unit of content within a message or artifact. It lists three interaction mechanisms — polling,
streaming and push notification — and a three-step flow: discover the A2A server's Agent Card, carry
out authorisation and authentication, then send an A2A request, either synchronous or streaming.

The same chapter treats discovery as the problem distributed deployment raises. It calls the Agent Card
a remote agent's digital business card, which the A2A client parses in order to discover that agent,
and names three ways of obtaining one: direct configuration, a fixed URI, and a registry. For the last
it describes Nacos acting as the A2A registry, managing agents' registration, discovery and retrieval
in one place, and supporting agent version management and gray releases, which it presents as making
distributed agent systems more maintainable and extensible.

A fifth source shows the discovery mechanism in use. Google's
[[BlogPosting/developers-guide-to-ai-agent-protocols]] introduces A2A as the answer to expertise that
lives with remote agents — potentially built by different teams, on different frameworks, running on
different servers — and notes that some data may never be exposed through an API at all but could be
exposed through an agentic interface. In its description each A2A agent publishes an Agent Card at the
well-known path `/.well-known/agent-card.json`, describing its name, capabilities and endpoint; the
calling agent fetches these cards to learn what each remote agent does and routes queries to the right
one at runtime, so adding a new remote agent is a matter of adding its URL, with no code change or
redeployment. The guide's worked example uses
[[SoftwareApplication/agent-development-kit]], whose `RemoteA2aAgent` routes to one remote agent per
turn; where a query spans several remote agents at once, the guide uses the `a2a-sdk` directly. The same
guide places A2A in a six-protocol stack and summarizes its role there in one line: MCP connects agents
to tools and data, and A2A connects agents to other agents. It also notes that the
[[DefinedTerm/universal-commerce-protocol]] reuses A2A's well-known-URL discovery pattern and can run over
A2A as a transport.

A survey of four emerging agent communication protocols,
[[ScholarlyArticle/a-survey-of-agent-interoperability-protocols]], summarizes A2A as enabling
peer-to-peer task delegation using capability-based Agent Cards, supporting secure and scalable
collaboration across enterprise agent workflows. It compares A2A with
[[DefinedTerm/model-context-protocol]], [[DefinedTerm/agent-communication-protocol]] and
[[DefinedTerm/agent-network-protocol]], and in the phased adoption roadmap it proposes, A2A is adopted
for collaborative task execution after MCP (for tool access) and ACP (for messaging), before adoption
extends to ANP for decentralized agent marketplaces.

## Related Terms

[[DefinedTerm/model-context-protocol]], [[DefinedTerm/ai-agent]], [[DefinedTerm/universal-commerce-protocol]],
[[DefinedTerm/agent-communication-protocol]], [[DefinedTerm/agent-network-protocol]]
