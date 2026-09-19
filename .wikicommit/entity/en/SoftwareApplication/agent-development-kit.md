---
title: "Agent Development Kit (ADK)"
type: "schema:SoftwareApplication"
lang: en
sources:
  - type: url
    url: 'https://developers.googleblog.com/build-better-ai-agents-5-developer-tips-from-the-agent-bake-off/'
    hash: sha256:1531476aa716dcaf43b35914743fee4765992073720af2d19e509b1086ea47f4
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"
tags: [agents, multi-agent-systems, agent-tooling]

properties:
  description: "A framework for building AI agents, distributed at adk.dev and presented by Google as one of its quickstart resources for building agent applications."
  applicationCategory: "Agent development framework"
  author: "[[Organization/google]]"
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
