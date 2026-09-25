---
title: "Agent Middleware"
type: "schema:BlogPosting"
lang: en
tags: [agent-frameworks, context-engineering, agent-architecture]
sources:
  - type: url
    url: 'https://blog.langchain.com/agent-middleware'
    hash: sha256:071e79d936c9e2d2b07b0eab257fff6823cbeb8a320c72649b9ca211b9cd7179
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A LangChain blog post introducing Middleware, the new agent abstraction in LangChain 1.0, as its answer to agent frameworks giving developers too little control over context engineering."
  author: ["The LangChain Team"]
  datePublished: "2025-09-08"
  publisher: "LangChain"
---

This post from the LangChain team announces [[DefinedTerm/agent-middleware]], the new agent
abstraction in [[SoftwareApplication/langchain]] 1.0, and argues why it was needed. Its diagnosis is
that the core agent abstraction — a model, a prompt and a list of tools, run in a loop that calls tools
until the model decides to stop — is simple to get running but hard to make flexible enough for
production, and that the hundreds of [[DefinedTerm/agent-framework]]s built on it share the weakness
the original LangChain agents had: too little control over [[DefinedTerm/context-engineering]], which
leads developers to leave the abstraction for custom code once a use case becomes non-trivial.

The post then recounts two years of attempts to fix this by adding parameters to the agent, explains
why that approach stopped scaling, and presents middleware as the replacement, available in the LangChain
1.0 alpha releases for Python and JavaScript.

## Key Points

- The post's answer to why agents built on frameworks are hard to make reliable is context engineering:
  what goes into the model determines what comes out, so reliability requires full control over the
  model's input.
- As complexity grows, it says, developers want to change three things: the agent's state beyond just
  messages, exactly what goes into the model, and the sequence of steps that runs.
- LangChain's earlier response was a succession of agent parameters: runtime configuration, custom state
  schemas, a function returning the prompt, a function returning the full message list, a pre-model
  hook (enabling things like summarizing long conversations), a post-model hook (enabling
  human-in-the-loop and guardrails), and a function choosing the model at each call.
- That approach is described as producing many parameters with dependencies on one another, which were
  hard to coordinate, hard to combine and hard to offer as off-the-shelf variants.
- Middleware keeps the core loop of a model node and a tool node and lets middleware specify
  `before_model`, `after_model` and `modify_model_request` hooks, plus custom state schemas and tools.
- Multiple middleware run like web-server middleware: in order on the way into the model call and in
  reverse order on the way back.
- LangChain states it will ship off-the-shelf middleware and maintain a list of community middleware,
  describing this as the collections of nodes developers had asked for to plug into LangGraph agents.
- The team reports having verified that middleware can replicate its separate LangGraph agent
  architectures — supervisor, swarm, bigtool, deepagents and reflection — and expects it to unify them.
- The alpha shipped three implementations already in use in LangChain's internal agents:
  human-in-the-loop (via `after_model`), summarization (via `before_model`) and Anthropic prompt caching
  (via `modify_model_request`).

## Context

The post is the vendor's own announcement of a feature in its framework, written during the 1.0 alpha;
its claim that middleware makes LangChain's the most flexible and composable agent abstraction
available is the vendor's assessment, and it reports no evaluation. It calls middleware the biggest new
part of LangChain 1.0 and asks for feedback.
