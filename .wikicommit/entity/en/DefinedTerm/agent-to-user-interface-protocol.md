---
title: "Agent-to-User Interface Protocol (A2UI)"
type: "schema:DefinedTerm"
lang: en
aliases: ["A2UI"]
tags: [agents, agent-protocols, generative-ui]
sources:
  - type: url
    url: 'https://developers.googleblog.com/developers-guide-to-ai-agent-protocols/'
    hash: sha256:7b380e1b02a7431f86ce85fd5ad5a49d2707ee157205f5584f28284782319fef
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A protocol that lets an AI agent compose user interfaces from a fixed catalog of safe component primitives in a declarative JSON format, sending the component structure and the data separately, for a client-side renderer to turn into native UI."
---

The Agent-to-User Interface Protocol (A2UI) is a protocol for letting an AI agent present its results as
an interface rather than as plain text. As described in
[[BlogPosting/developers-guide-to-ai-agent-protocols]], the agent dynamically composes novel layouts
from a fixed catalog, using a declarative JSON format made up of 18 safe component primitives such as
rows, columns and text fields, and a renderer on the client turns that JSON into native UI with
frameworks such as Lit, Flutter or Angular.

## Usage

The guide's motivating case is an agent that needs to show an inventory dashboard, an order form or a
supplier comparison, each of which would otherwise need its own hand-built frontend component. A2UI
separates the UI's structure from its data. The agent first creates a rendering surface, then sends
the component tree as a flat list of components that reference one another by ID rather than nesting,
and then sends a separate data payload; components bind to values in that payload by path, so data can
be updated without resending the components. In the guide's example, three prompts to the same agent
produce an inventory checklist, an order form and a supplier comparison from the same primitives, with
no additional frontend code.

During development, the web interface of [[SoftwareApplication/agent-development-kit]] (`adk web`) can
render A2UI components natively, so an agent's UI output can be tested without writing a custom
renderer.

The guide distinguishes A2UI from the [[DefinedTerm/agent-user-interaction-protocol]]: A2UI defines what
to render, while AG-UI defines how to stream an agent's events to the frontend.

## Related Terms

- [[DefinedTerm/agent-user-interaction-protocol]] — the streaming layer the guide pairs with A2UI
- [[DefinedTerm/model-context-protocol]] and [[DefinedTerm/agent2agent-protocol]] — the protocols the
  guide places on the tool and agent sides of the same agent
