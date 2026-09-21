---
title: "Agent Development Kit (ADK)"
type: "schema:SoftwareApplication"
lang: en
sources:
  - type: url
    url: 'https://developers.googleblog.com/build-better-ai-agents-5-developer-tips-from-the-agent-bake-off/'
    hash: sha256:1531476aa716dcaf43b35914743fee4765992073720af2d19e509b1086ea47f4
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/agent/multi-agent/'
    hash: sha256:644e8c22de6fd778cefa3c3c44647eee3beb025a3fb81617e0411c473018e2c9
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"
tags: [agents, multi-agent-systems, agent-tooling]

properties:
  description: "A framework for building AI agents, distributed at adk.dev and presented by Google as one of its quickstart resources for building agent applications. A second source places it as a coordination framework designed for hierarchical composition of specialised agents."
  applicationCategory: "Agent development framework"
  author: "[[Organization/google]]"
  featureList: "flexible orchestration patterns; hierarchical agent composition; a built-in evaluation framework; native Vertex AI integration; an Agent Starter Pack for production deployment"
---

The Agent Development Kit (ADK) is a framework for building AI agents, distributed at
adk.dev. Google presents it on its own developer blog as a quickstart resource for
building agent applications rather than assembling them from custom integration code,
and publishes documentation for using it to build multi-agent systems.

## Capabilities

Google's developer writing suggests ADK as the vehicle for building a multi-step agent
that layers in open agent protocols one at a time — the worked suggestion is a supply
chain agent for a restaurant that, as protocols are added, can check real inventory
databases, communicate with remote supplier agents, execute secure transactions and
render interactive, streaming dashboards. The framework is presented as something to
combine with open standards such as [[DefinedTerm/model-context-protocol]], and Google's
argument for it is that doing so avoids writing and maintaining brittle integration code
for every tool an agent touches.

Google distributes an accompanying Agent Starter Pack alongside it, described as a route
to deploying production-grade agents.

A chapter of Jimmy Song's online handbook 智能体构建指南, comparing six agent coordination
frameworks, names four strengths for ADK: flexible orchestration, support for hierarchical agent
composition, a built-in evaluation framework, and native Vertex AI integration. That chapter matches ADK
to the **hierarchical** architecture pattern — multiple layers of supervision in which upper layers
abstract complexity and lower ones carry out detail — naming it there alongside
[[SoftwareApplication/langgraph]], and saying ADK is particularly suited to it because it is designed
for composing specialised agents into modular, scalable applications. Its stated best use
there is building [[DefinedTerm/llm-based-multi-agent-system]]s on Google Cloud Platform. That
chapter gives no figure or measurement in support of its account of ADK.
