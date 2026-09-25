---
title: "Developer’s Guide to AI Agent Protocols"
type: "schema:BlogPosting"
lang: en
tags: [agents, agent-protocols, agent-tooling, multi-agent]
sources:
  - type: url
    url: 'https://developers.googleblog.com/developers-guide-to-ai-agent-protocols/'
    hash: sha256:7b380e1b02a7431f86ce85fd5ad5a49d2707ee157205f5584f28284782319fef
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A March 2026 post on Google's developer blog that explains six AI agent protocols — MCP, A2A, UCP, AP2, A2UI and AG-UI — by adding them one at a time to a restaurant supply-chain agent built with Agent Development Kit, presenting each as the removal of one kind of custom integration code."
  author: ["Shubham Saboo", "Kristopher Overholt"]
  publisher: "[[Organization/google]]"
  datePublished: "2026-03-18"
---

*Developer’s Guide to AI Agent Protocols*, published on Google's developer blog on 18 March 2026,
sets out to make sense of what it calls a landscape "overloaded with acronyms". Its authors take six
protocols — [[DefinedTerm/model-context-protocol]] (MCP), [[DefinedTerm/agent2agent-protocol]] (A2A),
the [[DefinedTerm/universal-commerce-protocol]] (UCP), the [[DefinedTerm/agent-payments-protocol]]
(AP2), the [[DefinedTerm/agent-to-user-interface-protocol]] (A2UI) and the
[[DefinedTerm/agent-user-interaction-protocol]] (AG-UI) — and argue that each saves the developer from
writing and maintaining custom integration code for one part of what an agent touches.

The post's method is a single worked example. Using [[SoftwareApplication/agent-development-kit]]
(ADK), it builds a kitchen-manager agent for a restaurant that orders wholesale ingredients, starting
from a bare LLM that "hallucinates everything" and adding one protocol per section until the agent can
check real inventory, get quotes from specialist agents, place orders, authorize payments and render
interactive, streaming dashboards. The authors chose the scenario because ordering ingredients needs
all of those capabilities at once. Every code sample uses ADK, and the post appears on Google's own
developer blog.

## Key Points

- MCP addresses connecting an agent to systems and data: rather than one custom tool per API endpoint,
  servers advertise their tools and the agent discovers them. The post adds that because MCP servers
  are maintained by the teams who built the underlying systems, the agent gets current tool
  definitions without the developer updating integration code.
- A2A addresses expertise held by remote agents that may be built by different teams, on different
  frameworks and servers. Each A2A agent publishes an Agent Card at a well-known URL describing its
  name, capabilities and endpoint, so adding a remote agent becomes a matter of adding its URL.
- UCP addresses the fact that every supplier has a different checkout API. It standardizes the
  shopping lifecycle into modular capabilities with strongly typed request and response schemas that
  stay the same whether the connection runs over REST, MCP, A2A or embedded protocols.
- AP2 addresses the question of who authorized a purchase. It adds typed mandates that provide
  non-repudiable proof of intent and enforce configurable guardrails, and plugs into UCP as an
  extension; the post notes AP2 is at v0.1 and ships as a separate package rather than in ADK core.
- A2UI addresses plain-text results where an interface is needed: the agent composes layouts from a
  fixed catalog of 18 component primitives in a declarative JSON format, and a client-side renderer
  turns them into native UI.
- AG-UI addresses the boilerplate of streaming agent events to a frontend, translating raw framework
  events into a standardized server-sent-events stream of typed events.
- In the worked example, one request exercises all six: MCP and A2A gather information, UCP and AP2
  complete the transaction, and A2UI and AG-UI present the result.
- The post's advice is to know which problem each protocol solves, add protocols only as
  requirements call for them (most agents, it says, start with MCP for data access), check for an ADK
  integration, official SDK and sample code before building, and adopt the standards early even
  though they are still maturing, because the patterns they share — discovery via well-known URLs,
  typed schemas and standard event streams — make an agent compatible with a growing ecosystem.

## Context

The post frames the six protocols as layers rather than competitors: its one-line summary is that MCP
connects agents to tools and data, A2A connects agents to other agents, UCP standardizes commerce, AP2
handles payment authorization, A2UI defines what to render and AG-UI defines how to stream it. It is
also a tutorial for Google's own framework: every code sample in the post uses ADK, and most protocol
sections point to an ADK integration for the protocol in question — AP2 being the exception, which the
post notes is not built into ADK core — so its recommendation to start from ADK integrations is the
publisher recommending its own tooling.
