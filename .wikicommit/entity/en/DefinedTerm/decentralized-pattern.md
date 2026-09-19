---
title: "Decentralized Pattern"
type: "schema:DefinedTerm"
lang: en
aliases: ["Agent handoffs"]
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
  description: "A multi-agent orchestration pattern in which agents operate as peers and hand workflow execution off to one another, transferring both control and conversation state so that the receiving agent takes over the interaction rather than reporting back."
---

The decentralized pattern is a multi-agent orchestration pattern in which agents operate on equal
footing and hand off workflow execution to one another based on their specializations. A handoff
is a one-way transfer: the agent that receives it takes over execution and interacts with the user
directly, rather than returning a result to whoever called it. It is one of two multi-agent
categories [[TechArticle/a-practical-guide-to-building-agents]] names as broadly applicable, the
other being the [[DefinedTerm/manager-pattern]].

## Usage

Modelled as a graph with agents as nodes, the decentralized pattern's edges are handoffs that
transfer execution, where the manager pattern's edges are tool calls that return. In the OpenAI
Agents SDK a handoff is itself a type of tool or function: when an agent calls it, execution
begins immediately on the agent handed off to, and the latest conversation state is transferred
with it (see [[SoftwareApplication/openai-agents-sdk]]).

The guide's worked example is a customer service workflow covering both sales and support. A
triage agent acts as the first point of contact, assessing queries and directing them to the right
specialist, with technical support, sales assistant and order management agents listed in its
`handoffs` array; a question about a recent purchase causes the triage agent to hand off to the
order management agent, transferring control to it. The guide notes the receiving agent can
optionally be equipped with a handoff back to the original agent.

## When It Applies

The guide presents the pattern as optimal where no single agent needs to maintain central control
or synthesize results — where it is acceptable, and preferable, for each agent to take over
execution and deal with the user itself. It names conversation triage as the archetypal case, and
more generally any scenario where specialized agents should fully take over certain tasks without
the original agent needing to stay involved.

It assumes a runtime that can carry conversation state across the transfer, since a handoff moves
the interaction rather than copying a task out and back. The guide's general precedence still
applies ahead of it: maximise a single agent's capabilities first, and introduce multiple agents
when prompts grow many conditional branches or tools overlap enough to confuse selection.

The pattern is one vendor's characterization of its own customer experience — the guide describes
these two categories as what its work with customers highlights — rather than an independently
established taxonomy, and its code examples assume that vendor's own SDK throughout.

## Related Terms

- [[DefinedTerm/manager-pattern]] — the other category the same guide names, where one agent keeps
  control and calls the others as tools
- [[DefinedTerm/agent-teams]]
- [[DefinedTerm/tool-use-design-pattern]]
