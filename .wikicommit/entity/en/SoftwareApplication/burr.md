---
title: "Burr"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-architecture, tool-use]
sources:
  - type: url
    url: 'https://blog.dagworks.io/p/agentic-design-pattern-1-tool-calling'
    hash: sha256:f5276fdca09410e46b0e304c27f4f41294afee574a8aae025568b5534898ad22
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A lightweight Python library from DAGWorks for building applications as state machines, used to structure LLM agents as a graph of actions with immutable state, paired with an open-source UI for monitoring and debugging."
  applicationCategory: "Agent orchestration framework"
  author: "DAGWorks Inc."
---

Burr is a lightweight Python library for building applications as state machines. An application is constructed from a series of *actions* — either decorated functions or objects — each of which declares the inputs it takes from state and from the user, contains custom logic that may delegate to any other framework, and specifies how it updates state. State is immutable, which its makers present as what allows it to be inspected at any point in a run. Actions are strung together with optionally conditional transitions, so an application can be viewed as a flow chart or graph, and Burr itself handles orchestration, monitoring and persistence.

Its makers, DAGWorks, position it for AI assistants, retrieval-augmented generation applications and human-in-the-loop AI interfaces, and describe its users as typically arriving after building a chatbot and then moving toward agents. The source used here is DAGWorks's own blog post, so the claims about what Burr adds are the vendor's.

## Capabilities

The [[DefinedTerm/tool-use-design-pattern]] walkthrough in that post exercises most of the library's surface. An action calls the model to choose a tool and returns which tool to run with what arguments; a `.bind()` feature then turns one parameterized tool-calling action into a separate action per tool, by binding a different value for the parameter each time — the post prefers this over a single dispatching action specifically so that every tool is visible in the graph. A final action formats the raw result for the user, and a transition loops back to the input so the next question can be asked.

Observability is described as a one-line change that pairs with an open-source user interface, in which state can be examined at any point, token counts viewed per step or span, and OpenTelemetry data for chat completions inspected. A `@trace()` decorator extends this into the tool functions themselves, so their invocations are logged to the same UI, and specific cases can be recreated as test cases. For production, the post names a persistence API for tracking sessions against a database of the reader's choice, and state-typing capabilities for deploying inside a FastAPI server.

## Adoption & Ecosystem

The post frames Burr's value as what it adds over writing the same API calls directly: because the workflow is a graph, it is self-documenting and readable; changes stay localized to specific actions and can be compared across runs; and graph-level concerns such as error conditions can be added as new actions and edges without touching existing code. The debugging argument is made specifically about tool calling — the post reports the model being finicky about choosing a tool at all and sometimes getting lost in the instructions, resolved through prompt engineering experimented on in Burr's UI.

The tool-calling example is written against OpenAI's API, which the post says extends straightforwardly to other providers, and Burr's role in it is described as a thin layer over whatever provider API supports tool or function calling.
