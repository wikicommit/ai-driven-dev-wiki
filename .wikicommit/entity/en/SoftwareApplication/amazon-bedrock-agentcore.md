---
title: "Amazon Bedrock AgentCore"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, context-window, aws, agent-runtime]
sources:
  - type: url
    url: 'https://aws.amazon.com/cn/blogs/china/agentic-ai-infrastructure-practice-series-nine-context-engineering/'
    hash: sha256:1ea97ed3d4e23cb29114ffee329716c05e979b914a7a52d5b181bf258202267f
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "AWS's enterprise platform for deploying and running agents, offered as a set of modular services — Runtime, Identity, Memory, Code Interpreter, Browser, Gateway and Observability — that are framework-agnostic, so an agent built on any framework can use them."
  applicationCategory: "Agent runtime platform"
  featureList: "Runtime; Identity; Memory (two-tier short-term and long-term); Code Interpreter; Browser; Gateway (tool gateway with semantic tool search); Observability"
  author: "Amazon Web Services"
---

Amazon Bedrock AgentCore is presented as AWS's enterprise-grade platform for developing and deploying agentic AI, occupying the runtime layer of the three-layer stack that [[BlogPosting/agentic-ai-infrastructure-context-engineering]] lays out — above the foundation models and above the agent framework. It is a set of modular services rather than a single product: Runtime, Identity, Memory, Code Interpreter, Browser, Gateway and Observability. Its stated advantage is compatibility with open-source frameworks alongside enterprise security, so a developer can use any framework and any model while relying on AWS for the infrastructure underneath.

Two of its components are treated in depth in that post because they address [[DefinedTerm/context-engineering]] problems directly: Memory, which decides what an agent carries between turns and between sessions, and Gateway, which decides how many tool definitions have to sit in the context window at once.

## Capabilities

**Memory** uses a two-tier architecture. Short-term memory stores conversational interactions to maintain the current session — the post's example is a coding-assistant agent recording variable inspections and syntax corrections so the conversation can continue without repeating information — and feeds the long-term tier. Long-term memory stores extracted insights under three strategies: user-preference memory (a developer's coding style, such as snake_case naming or a preference for pandas), semantic fact memory (accumulated domain knowledge), and summary memory (session summaries, which both track progress and reduce context-window usage). It is a fully managed SaaS service with multi-tenancy and data isolation, and integrates with LangGraph and CrewAI as well as with AWS's own framework.

**Gateway** converts existing APIs, Lambda functions and services into the MCP format an agent can call, which the post says removes weeks of custom integration work. Its notable mechanism is semantic tool search: rather than loading every tool definition into the context, the gateway retrieves the most relevant definitions for the task at hand, which the post presents as both cutting token usage and improving selection accuracy where a large tool catalogue would otherwise force a blind choice. It also carries versioning, IAM-based access control, usage monitoring and compliance auditing, with multi-layer caching across tool definitions, search results and call results.

## Adoption & Ecosystem

Within the post's architecture, AgentCore Runtime provides the execution environment and lifecycle management under which [[SoftwareApplication/strands-agents]] runs, while AgentCore Gateway coordinates that agent's tools. Strands Agents integrates AgentCore Memory through its hooks mechanism, so retrieval and storage of memories happen declaratively without touching the agent's own logic.

The post draws a deliberate contrast on when to reach for it: AgentCore Memory is presented as the better fit for enterprise deployment and strict compliance scenarios, while third-party memory services such as Mem0.ai integrated through Strands Agents are described as better suited to rapid prototyping and flexible customization.

Everything recorded here comes from a single post published by the vendor about its own products. For AgentCore specifically that post describes the services and shows Python for calling them without reporting any measurement of them — the cost figures it does give elsewhere concern Bedrock's prompt caching, not these components — and no independent evaluation of AgentCore appears.
