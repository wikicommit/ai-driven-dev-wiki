---
title: "Spring AI Alibaba"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-tooling, multi-agent, orchestration]
sources:
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-native-whitepaper/03-development-frameworks/'
    hash: sha256:387bad42083bfa6f2ac79781096a48796e1b0e141792328d9810971e043c1a93
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Java framework for developing AI agents, whose basic agent is a ReAct-style ReactAgent and which ships workflow agents (sequential, parallel, loop) and a model-routed multi-agent type."
  applicationCategory: "Agent development framework (Java)"
  featureList: "ReactAgent implementing the ReAct loop; FlowAgent-based SequentialAgent, ParallelAgent and LoopAgent for predefined workflows; LlmRoutingAgent for model-decided routing between sub-agents"
---

Spring AI Alibaba is a Java framework for building AI agents. Chapter 3 of the AI 原生应用架构白皮书
(AI-native application architecture whitepaper) hosted on jimmysong.io uses it as its worked example
of agent development, observing that the agent development ecosystem began mainly in Python and later
spread to languages such as Java, and presenting Java frameworks such as Spring AI Alibaba as giving
developers extensive agent-building capabilities.

That chapter uses the framework to illustrate three development paradigms: a single agent, which adds
retrieval, tools and memory to an LLM application (the chapter calls this an Augmented LLM Application —
see [[DefinedTerm/augmented-llm]]); a workflow, in which sub-agents are orchestrated along a predefined
flow; and a multi-agent system, in which the flow between agents is decided by the model and the
sub-agents collaborate with more autonomy (see [[DefinedTerm/llm-based-multi-agent-system]]).

## Capabilities

The framework's agent is defined as a **ReactAgent**, a typical implementation of the ReAct pattern
(see [[DefinedTerm/react-prompting]]): a loop of thought, in which the agent analyses the goal, what it
knows and which tools are available; action, in which it calls an external tool with a structured
instruction; and observation, in which the tool's result is fed back — repeated until the task is
complete. Defining an agent, as the chapter describes it, takes a name used as a unique identifier, a
description of its capabilities so that agents can be told apart in multi-agent settings, and a model,
with "qwen-max" given as an example. An `instruction` parameter guides its behaviour — the core task or
goal, a persona, behavioural constraints, instructions for using tools and the required output format —
and tools can be supplied as native functions, APIs or other agent instances.

The chapter's comparison of the framework's built-in agent types is:

| Type | Core behaviour | Flow orchestration | Determinism |
| --- | --- | --- | --- |
| ReactAgent | Reasoning, generation, tool use | None | Relatively high uncertainty |
| FlowAgent | Controls the flow of several agents | Predefined flow (sequential, parallel, etc.) | Relatively high determinism |
| MultiAgent | Controls the flow of several agents | Flow control that supports model decisions | Between ReactAgent and FlowAgent |

For workflows it describes three agent types. **SequentialAgent** runs sub-agents one after another, each
one's output becoming the next one's input; the example is a writing assistant made of a writer agent
and a reviewer agent. **ParallelAgent** runs sub-agents in parallel, suited to tasks spanning several
domains; the example is a search assistant whose domain-specific sub-agents run in parallel, with a
merger agent combining their output and the whole chained together with a SequentialAgent.
**LoopAgent** runs sub-agents repeatedly for tasks that need several rounds of iteration. For
model-driven multi-agent systems, **LlmRoutingAgent** lets the model decide which sub-agent the flow goes
to next, for dynamic flow control.

## Adoption & Ecosystem

The same chapter goes on to cover moving agents from a single process to distributed deployment through
the [[DefinedTerm/agent2agent-protocol]], with Nacos acting as a registry for agents, and message-driven
communication between agents built on RocketMQ. It presents these as the next stage after the in-process
patterns above rather than as features of the framework itself.
