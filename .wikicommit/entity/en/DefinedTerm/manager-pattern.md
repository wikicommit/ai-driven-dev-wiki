---
title: "Manager Pattern"
type: "schema:DefinedTerm"
lang: en
aliases: ["Agents as tools"]
tags: [agents, multi-agent, orchestration, agent-architecture]
sources:
  - type: url
    url: 'https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf'
    hash: sha256:9d619ed7dd7cb94569658ca3de72615ef792761e6e4147e36c45edf2f945bbf9
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A multi-agent orchestration pattern in which one central manager agent coordinates specialized agents by calling them as tools, keeping control of workflow execution and of the interaction with the user while synthesizing the specialists' results into a single response."
---

The manager pattern is a multi-agent orchestration pattern in which a central LLM — the manager —
coordinates a network of specialized agents by invoking them through tool calls, and synthesizes
their results into one coherent interaction. It is one of two multi-agent categories
[[TechArticle/a-practical-guide-to-building-agents]] names as broadly applicable, the other being
the [[DefinedTerm/decentralized-pattern]]; the guide also describes it as "agents as tools", since
an agent exposed to the manager is a tool from the manager's point of view.

## Usage

Modelled as a graph with agents as nodes, the manager pattern's edges are tool calls: the manager
delegates a task to the agent that fits it, receives the result, and remains the component that
speaks to the user. The guide's worked example is a translation agent whose manager holds three
specialists — Spanish, French and Italian — each registered as a tool with its own name and
description, so that a request for several translations becomes several tool calls from the same
manager. In the OpenAI Agents SDK the conversion is explicit: a specialist agent is turned into a
tool with `as_tool(...)`, given a tool name and a tool description, and listed in the manager's
`tools` array (see [[SoftwareApplication/openai-agents-sdk]]).

The guide treats agents-as-tools as one of three tool categories an agent may need, alongside data
tools that retrieve context and action tools that change something in an external system — so the
pattern is presented as an application of the ordinary
[[DefinedTerm/tool-use-design-pattern]] rather than as a separate mechanism.

## When It Applies

The guide presents the pattern as ideal for workflows where you want exactly one agent to control
workflow execution and to have access to the user. Its stated benefit follows from that: because
the manager never hands off control, it does not lose context, and specialized capabilities stay
available on demand behind a single, unified user experience.

Two assumptions come with it. The work has to decompose into tasks a specialist can complete and
return, since the manager's only way to reach a specialist is a tool call that comes back. And the
guide's broader advice applies first: it recommends maximising a single agent's capabilities
before introducing multiple agents at all, on the grounds that more agents provide intuitive
separation of concerns but add complexity and overhead, so a single agent with tools is often
sufficient. Its named triggers for splitting are prompts that have accumulated many conditional
branches and tools that overlap enough to confuse selection.

The pattern is one vendor's characterization of its own customer experience — the guide describes
these two categories as what its work with customers highlights — rather than an independently
established taxonomy, and its code examples assume that vendor's own SDK throughout.

## Related Terms

- [[DefinedTerm/decentralized-pattern]] — the other category the same guide names, where control
  transfers between peers instead of staying with one agent
- [[DefinedTerm/planner-worker-model]] — a separately reported hierarchical split of planning and
  implementation roles
- [[DefinedTerm/sub-agent-architecture]] — a related arrangement described in terms of context
  isolation rather than tool calls
- [[DefinedTerm/tool-use-design-pattern]]
