---
title: "Agent Communication Protocol (ACP)"
type: "schema:DefinedTerm"
lang: en
aliases: ["ACP"]
tags: [agents, agent-protocols, interoperability]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2505.02279'
    hash: sha256:7697852f9428f817d9c744137c1cc2162cddc7fa5d0876349a9b513835cce643
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An agent communication protocol that defines general-purpose communication over RESTful HTTP, supporting MIME-typed multipart messages and synchronous and asynchronous interactions, described in a 2025 survey as one of four emerging agent interoperability protocols."
---

The Agent Communication Protocol (ACP) is an agent communication protocol that defines general-purpose communication over RESTful HTTP, supporting MIME-typed multipart messages and both synchronous and asynchronous interactions. [[ScholarlyArticle/a-survey-of-agent-interoperability-protocols]] describes its design as lightweight and runtime-independent, which it says enables scalable agent invocation, and lists session management, message routing, and integration with role-based and decentralized identifiers (DIDs) among its features.

## Usage

That survey treats ACP as one of four emerging protocols for interoperability between LLM-powered agents, alongside [[DefinedTerm/model-context-protocol]], [[DefinedTerm/agent2agent-protocol]] and [[DefinedTerm/agent-network-protocol]]. In the phased adoption roadmap the survey proposes, ACP follows MCP: after MCP is adopted for tool access, ACP is introduced for structured, multimodal, session-aware messaging, and the survey also associates this stage with both online and offline agent discovery across scalable, HTTP-based deployments.

## Related Terms

- [[DefinedTerm/model-context-protocol]] — the protocol the survey's roadmap adopts first, for tool access
- [[DefinedTerm/agent2agent-protocol]] — the protocol the roadmap adds for collaborative task execution
- [[DefinedTerm/agent-network-protocol]] — the protocol the roadmap extends to for decentralized agent marketplaces
