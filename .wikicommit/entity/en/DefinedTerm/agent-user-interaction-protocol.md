---
title: "Agent-User Interaction Protocol (AG-UI)"
type: "schema:DefinedTerm"
lang: en
aliases: ["AG-UI"]
tags: [agents, agent-protocols, streaming]
sources:
  - type: url
    url: 'https://developers.googleblog.com/developers-guide-to-ai-agent-protocols/'
    hash: sha256:7b380e1b02a7431f86ce85fd5ad5a49d2707ee157205f5584f28284782319fef
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A protocol that acts as middleware between an agent framework and a frontend, translating raw framework events into a standardized server-sent-events stream of typed events so that the frontend does not depend on which framework produced them."
---

The Agent-User Interaction Protocol (AG-UI) is a protocol for connecting an AI agent to a frontend.
[[BlogPosting/developers-guide-to-ai-agent-protocols]] describes it as middleware that translates raw
agent-framework events into a standardized server-sent events (SSE) stream, so that a frontend can
listen for typed events — its examples include `TEXT_MESSAGE_CONTENT` and `TOOL_CALL_START` — without
caring which agent framework produced them.

## Usage

The guide's case for AG-UI starts from how agents differ from traditional REST APIs: a REST call returns
a response and is done, whereas an agent streams text incrementally, calls tools in the middle of a
response and sometimes pauses to wait for human input. A developer can handle this directly — the guide
notes that [[SoftwareApplication/agent-development-kit]] provides a native `/run_sse` endpoint and that a
few dozen lines of frontend code can parse the stream — but calls that parsing code boilerplate that
breaks whenever the event format changes. AG-UI removes that boilerplate.

In the guide's example, an ADK agent is wrapped with the `ag_ui_adk` package and mounted as an endpoint
on a FastAPI app. The resulting stream opens with a run-started event, reports each tool call with start,
result and end events, delivers text as a series of message-content deltas, and closes with a
run-finished event.

The guide distinguishes AG-UI from the [[DefinedTerm/agent-to-user-interface-protocol]]: A2UI defines what
to render, and AG-UI defines how to stream it.

## Related Terms

- [[DefinedTerm/agent-to-user-interface-protocol]] — the UI-composition layer the guide pairs with AG-UI
- [[DefinedTerm/human-in-the-loop]] — one of the agent behaviours, pausing for human input, that the
  guide says makes agent frontends harder than REST frontends
