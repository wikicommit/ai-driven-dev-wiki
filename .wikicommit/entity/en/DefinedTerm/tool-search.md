---
title: "Tool search"
type: "schema:DefinedTerm"
lang: en
tags: [tool-use, agent-tooling, context-engineering]
sources:
  - type: url
    url: 'https://platform.openai.com/docs/guides/function-calling'
    hash: sha256:837fddfb4f47440271a02bb4e3bf476c552ccbfc1b962b602a0217dc5bf68f47
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A technique for giving a model access to a large set of tools without loading them all up front: some or all tools are deferred, and the model searches for the relevant ones, adds them to its context and then calls them."
---

Tool search is a way of giving a model access to a large ecosystem of tools without placing every tool
definition in its context from the start. Some or all tools are **deferred**; the model searches for the
tools relevant to the task, loads them into its context, and then uses them like any other tool. In
OpenAI's function-calling guide it appears as the `tool_search` tool, offered as the answer when an
application has many functions or large schemas, and as the way to keep the number of initially
available functions small while still exposing a large tool surface.

## Usage

The motivation the guide gives is cost and accuracy. Function definitions are injected into the model's
context, so they count against the context limit and are billed as input tokens, and the guide
recommends keeping the functions available at the start of a turn few for higher accuracy. Deferring
large or infrequently used parts of the tool surface addresses both. When tool search is in use, the
model's output may contain tool-search call and output items before a function call; once a function
has been loaded it is handled like any other call, and `tool_choice` constrains only the tools currently
callable in that turn.

Tool search interacts with how tools are described. Where deferred tools are grouped into namespaces
(see [[DefinedTerm/tool-namespacing]]), the guide advises keeping the namespace description concise and
putting the detailed guidance in each function's description: the namespace helps the model decide what
to load, and the function description helps it use the loaded tool correctly. OpenAI states that only
`gpt-5.4` and later models support `tool_search`.

## Related Terms

- [[DefinedTerm/function-calling]]
- [[DefinedTerm/tool-namespacing]]
- [[DefinedTerm/virtual-tools]]
- [[DefinedTerm/embedding-guided-tool-routing]]
- [[DefinedTerm/context-engineering]]
