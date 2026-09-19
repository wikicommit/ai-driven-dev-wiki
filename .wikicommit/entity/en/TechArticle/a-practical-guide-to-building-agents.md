---
title: "A practical guide to building agents"
type: "schema:TechArticle"
lang: en
tags: [agents, agent-architecture, guardrails, orchestration]
sources:
  - type: url
    url: 'https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf'
    hash: sha256:9d619ed7dd7cb94569658ca3de72615ef792761e6e4147e36c45edf2f945bbf9
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "OpenAI's guide for product and engineering teams building their first agents, distilling its customer deployments into a definition of an agent, criteria for when to build one, the model/tools/instructions foundations, single- and multi-agent orchestration patterns, and a layered treatment of guardrails."
  publisher: "OpenAI"
---

*A practical guide to building agents* is a guide published by OpenAI for product and engineering
teams exploring how to build their first agents. It presents itself as distilling insights from
numerous customer deployments into practical and actionable best practices, covering frameworks
for identifying promising use cases, patterns for designing agent logic and orchestration, and
practices intended to keep agents running safely and predictably.

Its stated scope is deliberately foundational: after reading it, the guide says, the reader will
have the knowledge needed to start building a first agent. It is organised into five parts — what
an agent is, when to build one, agent design foundations, guardrails, and a conclusion — and
illustrates each design point with short Python examples written against
[[SoftwareApplication/openai-agents-sdk]], while noting the same concepts can be implemented with
any preferred library or from scratch.

## Details

The guide defines agents as systems that independently accomplish tasks on a user's behalf, and
draws the line at workflow control: applications that integrate LLMs but do not use them to
control workflow execution — simple chatbots, single-turn LLMs, sentiment classifiers — are not
agents. It gives an agent two core characteristics: it uses an LLM to manage workflow execution
and decide when a workflow is complete, correcting its actions or halting and returning control to
the user on failure; and it has access to tools with which to interact with external systems,
selecting among them dynamically and always within defined guardrails.

On when to build one, the guide argues agents suit workflows that have resisted conventional
automation, and names three: complex workflows involving nuanced judgment or exceptions, systems
made difficult to maintain by extensive and intricate rulesets, and workflows relying heavily on
unstructured data. Its worked contrast is payment fraud analysis, where a traditional rules engine
works like a checklist while an LLM agent evaluates context and subtle patterns. Where a use case
does not clearly meet these criteria, the guide says a deterministic solution may suffice.

Its design foundations are three components — the model powering reasoning, the tools the agent
can call, and the instructions defining its behaviour. It recommends prototyping with the most
capable model for every task to establish a baseline, then swapping in smaller models to find
where they still suffice. Tools are grouped into data, action and orchestration tools, the last
being agents exposed as tools to other agents. For instructions, it recommends deriving routines
from existing operating procedures and policy documents, breaking dense resources into smaller
steps, making every step correspond to a specific action or output, and anticipating edge cases
with conditional branches.

Orchestration is presented as a choice between single-agent systems, in which one model equipped
with tools runs in a loop until an exit condition is reached, and multi-agent systems. The guide's
general recommendation is to maximise a single agent's capabilities first, adding tools
incrementally, and to reach for multiple agents when prompts accumulate many conditional branches
or when tools overlap enough to confuse selection — noting that the issue is tool similarity
rather than tool count, with some implementations managing more than 15 distinct tools and others
struggling with fewer than 10 overlapping ones. Where multiple agents are warranted, it names two
broadly applicable categories: the [[DefinedTerm/manager-pattern]] and the
[[DefinedTerm/decentralized-pattern]].

The final section treats [[DefinedTerm/guardrails]] as a layered defence rather than a single
control, combining LLM-based classifiers, rules-based protections such as regex and blocklists,
and a moderation API. It lists seven types — relevance classifier, safety classifier, PII filter,
moderation, tool safeguards, rules-based protections and output validation — and offers a
three-step heuristic for building them: focus first on data privacy and content safety, add
guardrails as real-world edge cases and failures appear, and tune for both security and user
experience as the agent evolves. It closes by treating [[DefinedTerm/human-in-the-loop]]
intervention as a critical safeguard, especially early in deployment, triggered by exceeding
failure thresholds or by high-risk actions.
