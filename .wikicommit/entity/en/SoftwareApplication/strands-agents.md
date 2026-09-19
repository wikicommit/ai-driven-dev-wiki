---
title: "Strands Agents"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-frameworks, tool-use]
sources:
  - type: url
    url: 'https://dev.to/aws/ai-agent-guardrails-rules-that-llms-cannot-bypass-596d'
    hash: sha256:d321340a9dfb2556bc45605cd43311d6f886dd3c139f618c6380e18345aa7a1a
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A Python agent framework whose hook system lets a developer intercept a tool call before it executes and cancel it, so constraints can be enforced outside the language model rather than stated to it in a prompt."
  applicationCategory: "Agent framework"
  featureList: "BeforeToolCallEvent pre-execution hook; HookProvider/HookRegistry callback registration; event.cancel_tool call cancellation; pluggable model providers; @tool-decorated tool definitions"
---

Strands Agents is a Python framework for building tool-using LLM agents. An agent is constructed with a list of tools and a model, and tools are ordinary Python functions marked with a `@tool` decorator, their docstrings serving as the description the model sees.

The capability it is discussed for here is its hook system. A `HookProvider` registers callbacks against lifecycle events through a `HookRegistry`, and `BeforeToolCallEvent` fires before a tool call executes. A callback on that event receives the pending call — its name and its input — and can stop it by assigning a message to `event.cancel_tool`, at which point the framework substitutes that message for the tool's result and the tool never runs. Because the callback executes outside the model, the model receives the cancellation as the outcome of its call and cannot retry around it with different parameters.

## Capabilities

- Agents are constructed from a list of tools and a model; attaching interception is a single additional `hooks=[...]` argument, leaving the tool definitions and prompts untouched.
- Tools are plain functions decorated with `@tool`, needing no validation logic mixed into them.
- `BeforeToolCallEvent` exposes the pending tool call for inspection before execution, and `event.cancel_tool` cancels it with an explanatory message returned to the model in place of a result.
- The model provider is configurable; the example discussed here runs on OpenAI GPT-4o-mini by default and the framework's documentation covers the other providers it supports.

## Adoption & Ecosystem

The framework appears here as the vehicle for a [[DefinedTerm/neurosymbolic-validation]] pattern, in which deterministic business rules are evaluated in a hook and enforced before a tool executes rather than stated to the model in a prompt or docstring. Its hook mechanism is one implementation of the interception point described under [[DefinedTerm/agent-hooks]]; equivalents in other agent frameworks are named alongside it as LangGraph node guards and AutoGen reply functions. The account summarized here comes from a single post published under the AWS organization, which uses the framework rather than documenting it, so it establishes the hook API used in that example and little else about the project.
