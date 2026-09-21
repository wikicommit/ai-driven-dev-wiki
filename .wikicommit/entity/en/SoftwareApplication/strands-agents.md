---
title: "Strands Agents"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-frameworks, tool-use, context-window]
sources:
  - type: url
    url: 'https://dev.to/aws/ai-agent-guardrails-rules-that-llms-cannot-bypass-596d'
    hash: sha256:d321340a9dfb2556bc45605cd43311d6f886dd3c139f618c6380e18345aa7a1a
  - type: url
    url: 'https://aws.amazon.com/cn/blogs/china/agentic-ai-infrastructure-practice-series-nine-context-engineering/'
    hash: sha256:1ea97ed3d4e23cb29114ffee329716c05e979b914a7a52d5b181bf258202267f
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A lightweight, code-first Python framework for building tool-using LLM agents, defaulting to Amazon Bedrock and Claude. Its hook system lets a developer intercept a tool call before it executes and cancel it, and its conversation managers decide what of a growing history stays in the context window."
  applicationCategory: "Agent framework"
  featureList: "BeforeToolCallEvent pre-execution hook; HookProvider/HookRegistry callback registration; event.cancel_tool call cancellation; NullConversationManager, SlidingWindowConversationManager and summarizing conversation management; pluggable model providers; @tool-decorated tool definitions"
---

Strands Agents is a Python framework for building tool-using LLM agents, described as lightweight and code-first, with production-ready support for multiple model providers and deployment targets and Amazon Bedrock with Claude models as its default integration. An agent is constructed with a list of tools and a model, and tools are ordinary Python functions marked with a `@tool` decorator, their docstrings serving as the description the model sees. It supports conversational and non-conversational agents, streaming and non-streaming responses, and ships with observability, tracing and security features.

Two capabilities are documented here from different sources. The first is its hook system: a `HookProvider` registers callbacks against lifecycle events through a `HookRegistry`, and `BeforeToolCallEvent` fires before a tool call executes. A callback on that event receives the pending call — its name and its input — and can stop it by assigning a message to `event.cancel_tool`, at which point the framework substitutes that message for the tool's result and the tool never runs. Because the callback executes outside the model, the model receives the cancellation as the outcome of its call and cannot retry around it with different parameters.

The second is conversation management, the framework's answer to a [[DefinedTerm/context-engineering]] problem: context accumulates as an interaction proceeds, and unmanaged it causes window overflow, response latency and rising cost.

## Capabilities

- Agents are constructed from a list of tools and a model; attaching interception is a single additional `hooks=[...]` argument, leaving the tool definitions and prompts untouched.
- Tools are plain functions decorated with `@tool`, needing no validation logic mixed into them.
- `BeforeToolCallEvent` exposes the pending tool call for inspection before execution, and `event.cancel_tool` cancels it with an explanatory message returned to the model in place of a result.
- The model provider is configurable; the example discussed in the first source runs on OpenAI GPT-4o-mini by default and the framework's documentation covers the other providers it supports.
- Three conversation-management modes, each embodying a different policy on what to keep. `NullConversationManager` retains everything, offered for short interactions, debugging, research use and compliance scenarios needing the full record. `SlidingWindowConversationManager` keeps a fixed number of recent turns on the assumption that recent conversation is more relevant than older conversation, with a `should_truncate_results` option for over-long tool results. A summarizing manager is offered for cases where older content should be condensed rather than dropped.
- The hooks mechanism doubles as a memory integration point: retrieval hooks inject relevant memories into the user message and storage hooks save new conversational content, keeping both out of the agent's business logic.

## Adoption & Ecosystem

The framework appears in the first source as the vehicle for a [[DefinedTerm/neurosymbolic-validation]] pattern, in which deterministic business rules are evaluated in a hook and enforced before a tool executes rather than stated to the model in a prompt or docstring. Its hook mechanism is one implementation of the interception point described under [[DefinedTerm/agent-hooks]]; equivalents in other agent frameworks are named alongside it as LangGraph node guards and AutoGen reply functions. That account comes from a single post published under the AWS organization, which uses the framework rather than documenting it, so it establishes the hook API used in that example and little else about the project.

[[BlogPosting/agentic-ai-infrastructure-context-engineering]] places it at the agent-framework layer of AWS's context-engineering stack, between Amazon Bedrock beneath it and [[SoftwareApplication/amazon-bedrock-agentcore]] above, and describes its memory management integrating with AgentCore Memory through those same hooks. That post also contrasts the two: AgentCore Memory is presented as suiting enterprise deployment and strict compliance, while third-party memory services such as Mem0.ai reached through Strands Agents are presented as suiting rapid prototyping and flexible customization. Both sources for this page are published by AWS, one on a community platform and one on the company's own blog, so nothing here is an independent assessment of the framework.
