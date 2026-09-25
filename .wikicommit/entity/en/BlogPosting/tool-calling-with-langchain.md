---
title: "Tool Calling with LangChain"
type: "schema:BlogPosting"
lang: en
tags: [tool-use, agent-frameworks, llm]
sources:
  - type: url
    url: 'https://blog.langchain.com/tool-calling-with-langchain/'
    hash: sha256:272d889d15308a542b7029c3aae6528c22e13a794ef6e75763f377ff9e0b206a
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An April 2024 LangChain blog post introducing a provider-independent interface for tool calling — bind_tools, a tool_calls attribute on AIMessage, and create_tool_calling_agent — after model providers had shipped native tool calling through incompatible APIs."
  author: ["The LangChain Team"]
  datePublished: "2024-04-11"
  publisher: "LangChain"
---

This post from the LangChain team introduces a standard interface in [[SoftwareApplication/langchain]]
for tool calling, the capability that lets a model return a list of tool invocations alongside or instead
of plain text (see [[DefinedTerm/tool-use-design-pattern]]). Its occasion was that more and more model
providers were exposing native tool calling, each through a slightly different interface — including,
the post notes, the three it calls the highest-performing, OpenAI, Anthropic and Gemini, which were
incompatible with one another — and that the community wanted a standard way to switch between them.

The interface has three parts: `ChatModel.bind_tools()` for attaching tool definitions to model calls,
an `AIMessage.tool_calls` attribute for reading the tool calls a model decided to make, and
`create_tool_calling_agent()`, an agent constructor that works with any model implementing both. The
post states that it is fully backwards compatible and supported on all models with native tool-calling
support.

## Key Points

- The post dates native tool calling to OpenAI's "function calling", released roughly a year before
  the post and evolving into "tool calling" in November; it lists Gemini, Mistral, Fireworks, Together,
  Groq, Cohere and Anthropic as following between December and April.
- Tool definition formats differ by provider — OpenAI expects `name`, `description` and `parameters`,
  Anthropic `name`, `description` and `input_schema` — and `bind_tools` accepts raw definitions as well
  as Pydantic classes, LangChain tools and plain functions, so the same definitions can be used with any
  tool-calling model.
- Tool invocations had previously been found in `AIMessage.additional_kwargs` or `AIMessage.content`
  in a provider-specific format; `tool_calls` returns them as a list of `ToolCall` entries, each carrying
  a name, arguments and an optional id.
- `create_tool_calling_agent()` generalizes the earlier `create_openai_tools_agent()`, which worked only
  with models following OpenAI's tool-calling API.
- The same interface simplifies building agents in [[SoftwareApplication/langgraph]].
- `with_structured_output()` is built on tool calling for most models that support it: it always returns
  output in a given schema, which suits information extraction, whereas `bind_tools` lets the model pick
  one tool, several, or none, which suits agents that must also respond to the user.

## Context

The post is the vendor's announcement of a change to its own framework and says it expects the trend
toward native tool calling in models to continue.
