---
title: "A survey of agent interoperability protocols: Model Context Protocol (MCP), Agent Communication Protocol (ACP), Agent-to-Agent Protocol (A2A), and Agent Network Protocol (ANP)"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, agent-protocols, multi-agent, interoperability]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2505.02279'
    hash: sha256:7697852f9428f817d9c744137c1cc2162cddc7fa5d0876349a9b513835cce643
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A 2025 arXiv survey that examines four emerging communication protocols for LLM-powered agents (MCP, ACP, A2A and ANP), compares them across interaction modes, discovery mechanisms, communication patterns and security models, and proposes a phased adoption roadmap."
  author: ["Abul Ehtesham", "Aditi Singh", "Gaurav Kumar Gupta", "Saket Kumar"]
  datePublished: "2025-05-04"
  keywords: ["agent interoperability", "Model Context Protocol", "Agent Communication Protocol", "Agent-to-Agent Protocol", "Agent Network Protocol"]
---

This survey starts from the argument that autonomous agents powered by large language models need robust, standardized protocols to integrate tools, share contextual data and coordinate tasks across heterogeneous systems, because ad-hoc integrations are difficult to scale, secure and generalize across domains. It examines four emerging agent communication protocols, each addressing interoperability in a different deployment context: [[DefinedTerm/model-context-protocol]] (MCP), [[DefinedTerm/agent-communication-protocol]] (ACP), [[DefinedTerm/agent2agent-protocol]] (A2A) and [[DefinedTerm/agent-network-protocol]] (ANP).

The paper compares the four protocols across interaction modes, discovery mechanisms, communication patterns and security models, and on the basis of that comparison proposes a phased adoption roadmap: MCP first for tool access, then ACP for structured, multimodal, session-aware messaging, then A2A for collaborative task execution, and finally ANP for decentralized agent marketplaces. The authors present the work as a foundation for designing secure, interoperable and scalable ecosystems of LLM-powered agents.

## Key Points

- MCP provides a JSON-RPC client-server interface for secure tool invocation and typed data exchange.
- ACP defines a general-purpose communication protocol over RESTful HTTP that supports MIME-typed multipart messages and both synchronous and asynchronous interactions.
- A2A enables peer-to-peer task delegation using capability-based Agent Cards, supporting collaboration across enterprise agent workflows.
- ANP supports open-network agent discovery and secure collaboration using W3C decentralized identifiers (DIDs) and JSON-LD graphs.
- The protocols are compared across interaction modes, discovery mechanisms, communication patterns and security models.
- The proposed adoption roadmap is phased: MCP for tool access, then ACP, then A2A, then ANP for decentralized agent marketplaces.

## Notes

The paper was first submitted to arXiv on 4 May 2025 and revised on 23 May 2025 (version 2). It is listed under Artificial Intelligence (cs.AI).
