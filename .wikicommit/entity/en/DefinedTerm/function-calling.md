---
title: "Function calling"
type: "schema:DefinedTerm"
lang: en
aliases: ["Tool calling"]
tags: [tool-use, agent-tooling, llm-api]
sources:
  - type: url
    url: 'https://platform.openai.com/docs/guides/function-calling'
    hash: sha256:837fddfb4f47440271a02bb4e3bf476c552ccbfc1b962b602a0217dc5bf68f47
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A model capability, also called tool calling, in which an application describes the tools a model may use and the model responds with a structured request to call one, which the application executes and returns to the model before it produces its final answer."
---

Function calling, also known as tool calling, is the mechanism by which a language model interfaces
with external systems and data outside its training data. The application tells the model which
**tools** it has access to — a function is a kind of tool defined by a JSON schema for its inputs — and
the model, when it judges that following a prompt needs one of them, responds with a **tool call**
naming the tool and its arguments instead of a final answer. The application executes the call, sends
the **tool call output** back referencing that call, and the model then answers or makes further calls.
OpenAI's API guide describes this as a multi-step conversation between the application and the model in
five steps: request with tools, receive a tool call, execute it on the application side, send the output
back, and receive a final response or more tool calls.

## Usage

In OpenAI's API a function definition has a type, a name, a description of when and how to use it, a
JSON Schema for its parameters, and a `strict` flag. Beyond JSON-schema function tools, the guide
describes *custom tools*, which take and return free-form text and can have that input constrained by a
context-free grammar (in a Lark variant or as a regular expression), and built-in platform tools such as
web search, code execution and access to [[DefinedTerm/model-context-protocol]] servers. Related tools
can be grouped into namespaces (see [[DefinedTerm/tool-namespacing]]), and rarely used ones deferred
with [[DefinedTerm/tool-search]] so that they are loaded only when the model needs them.

The guide's recommendations for defining functions are to write clear names, parameter descriptions and
instructions, including when not to use a function; to apply ordinary software-engineering practice,
such as using enums and object structure so invalid states cannot be expressed and checking whether a
human intern could use the function from the description alone; to keep arguments the application
already knows out of the model's hands and to merge functions that are always called in sequence; and to
keep the number of functions available at the start of a turn small, suggesting fewer than 20 as a soft
guide. It notes that function definitions are injected into the model's context, so they count against
the context limit and are billed as input tokens.

Several controls shape how calls are made. `tool_choice` lets the application leave the decision to the
model, require at least one call, force one specific function, restrict calls to an allowed subset, or
disable calls. A model may call several functions in one turn unless parallel calls are turned off.
*Strict mode* makes calls reliably conform to the schema by building on structured outputs, which
requires every object to forbid additional properties and every field to be marked required; OpenAI
recommends always enabling it. Results are usually returned as a string in whatever format the
application chooses, and a function with no return value should still report success or failure.

## Related Terms

- [[DefinedTerm/tool-use-design-pattern]]
- [[DefinedTerm/agentic-tool-use]]
- [[DefinedTerm/tool-namespacing]]
- [[DefinedTerm/tool-search]]
- [[DefinedTerm/programmatic-tool-calling]]
- [[DefinedTerm/client-and-server-tools]]
