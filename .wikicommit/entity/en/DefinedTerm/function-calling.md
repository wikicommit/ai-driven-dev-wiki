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
  - type: url
    url: 'https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/how-tool-use-works'
    hash: sha256:72962bc6dbde244cd4d2ed36591f00bceb8f38f4883c0f7c11aaaafd13504b19
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

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
back, and receive a final response or more tool calls. Anthropic's conceptual guide to tool use in the
Claude API describes the same exchange as a contract: the application specifies which operations are
available and what shape their inputs and outputs take, the model decides when and how to call them, and
the model never executes anything on its own — it emits a structured request, the application's code (or
Anthropic's servers) runs the operation, and the result flows back into the conversation.

## Usage

In OpenAI's API a function definition has a type, a name, a description of when and how to use it, a
JSON Schema for its parameters, and a `strict` flag. Beyond JSON-schema function tools, the guide
describes *custom tools*, which take and return free-form text and can have that input constrained by a
context-free grammar (in a Lark variant or as a regular expression), and built-in platform tools such as
web search, code execution and access to [[DefinedTerm/model-context-protocol]] servers. Related tools
can be grouped into namespaces (see [[DefinedTerm/tool-namespacing]]), and rarely used ones deferred
with [[DefinedTerm/tool-search]] so that they are loaded only when the model needs them.

In Anthropic's Claude API the model's request arrives as a `tool_use` block carrying the tool name and a
JSON object of arguments, and the application returns the output in a `tool_result` block on the next
request. Anthropic's guide says this makes the model behave less like a text generator and more like a
function the application calls, so that engineers used to classical APIs can integrate it like any
other typed interface — define the schema, handle the callback, return a result — the difference being
that the caller choosing which function to invoke is a language model reading the conversation. It
describes the canonical shape of the resulting loop as a `while` loop keyed on `stop_reason`: while the
response stops with `"tool_use"`, execute the requested tools and continue the conversation, and exit on
any other stop reason. The same guide sorts tools by where their code runs, which decides whether the
application has to drive that loop at all (see [[DefinedTerm/client-and-server-tools]]).

The OpenAI guide's recommendations for defining functions are to write clear names, parameter descriptions and
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

Anthropic's guide also states when tool use fits: when a task needs something the model cannot do from text
alone — actions with side effects such as sending an email or writing a file, fresh or external data
such as current prices or the contents of a database, structured output of a guaranteed shape, and calls
into existing systems such as internal APIs or filesystems. It offers a rule of thumb: an application
that writes a regular expression to extract a decision from model output should have made that decision
a tool call. It also states when tool use does not fit: when the model can answer from training alone
(summarization, translation, general-knowledge questions), when the interaction is one-shot question and
answer with nothing to execute, and when the latency of at least one extra round trip per call would
outweigh a trivial task. These criteria are one vendor's guidance in its own documentation.

## Related Terms

- [[DefinedTerm/tool-use-design-pattern]]
- [[DefinedTerm/agentic-tool-use]]
- [[DefinedTerm/tool-namespacing]]
- [[DefinedTerm/tool-search]]
- [[DefinedTerm/programmatic-tool-calling]]
- [[DefinedTerm/client-and-server-tools]]
