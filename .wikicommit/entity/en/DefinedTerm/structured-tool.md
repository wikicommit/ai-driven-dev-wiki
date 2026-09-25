---
title: "Structured Tool"
type: "schema:DefinedTerm"
lang: en
aliases: ["StructuredTool"]
tags: [tool-use, agent-frameworks]
sources:
  - type: url
    url: 'https://blog.langchain.com/structured-tools/'
    hash: sha256:e4617b3533e7c5a963a20bc2b7e5763d3a2a4cfe73dd16914c5abd6772686b08
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "LangChain's abstraction for a tool that takes any number of typed inputs, defined by a name, a description, an argument schema and the functions that run it, as opposed to earlier tools that accepted a single string."
---

A structured tool is LangChain's abstraction, introduced in May 2023, for an action an agent can take
that accepts an arbitrary number of inputs of arbitrary types rather than a single input string. It wraps
a function so that an agent can call it, and is defined by four parts: a `name` that tells the agent
which tool to pick, a `description` explaining when and why to use it, an `args_schema` — a Pydantic
model declaring the arguments and their types — and `_run` and `_arun` functions holding the tool's
synchronous and asynchronous logic.

## Usage

The term belongs to [[SoftwareApplication/langchain]], where the `StructuredTool` class was announced in
[[BlogPosting/structured-tools]]. The `args_schema` does two jobs on LangChain's account: it tells the
agent what information the tool needs, and it validates the agent's inputs before the tool runs. A tool
can be built from a plain function with `StructuredTool.from_function()`, which infers the schema from
the function's signature, or by subclassing `BaseTool` for more control. It did not replace the earlier string tool: the original `Tool` class shares a base class with `StructuredTool`,
and a tool that takes one string argument is still treated as a string tool. LangChain released a
`StructuredChatAgent` to use such tools, because the prompts and output parsers of its earlier agents
did not work with multi-argument tools without customization.

## Related Terms

- [[DefinedTerm/tool-use-design-pattern]]
- [[DefinedTerm/react-prompting]]
