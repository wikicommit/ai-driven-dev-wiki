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
  - type: url
    url: 'https://simonwillison.net/2023/Jun/13/function-calling/'
    hash: sha256:e7d11c6a285c986f69ed52dd7b2da7c46a0d718252d9ca84ac6df6de515e6516
  - type: url
    url: 'https://simonwillison.net/2025/May/27/llm-tools/'
    hash: sha256:a2f0dcf34a578fc6603991e91422876e38f9d81009a3891d641eb6b221e19cde
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

## Introduction and Early Reception

A link post by Simon Willison dated 13 June 2023 records OpenAI announcing function calling that day,
among other API updates, for GPT-3.5 and GPT-4. As that post describes it, a developer sends a JSON
schema defining one or more functions, and the model returns a blob of JSON describing a function it
wants called, if it determines that one should be; the developer's code executes the function and
passes the result back to the model so that execution continues. Willison characterised this as
effectively an implementation of the [[DefinedTerm/react-prompting]] pattern, with models that have
been fine-tuned to execute it. He also noted that OpenAI's announcement acknowledged the risk of
[[DefinedTerm/prompt-injection]], though not by name, quoting its advice that developers can protect
their applications by only consuming information from trusted tools and by including user
confirmation steps before actions with real-world impact, such as sending an email, posting online or
making a purchase.

Writing in May 2025, in [[BlogPosting/large-language-models-can-run-tools-in-your-terminal-with-llm-0-26]],
Willison describes the same mechanism as having become, in his view, the single most effective way to
extend what language models can do, and as a simple trick: the model is told which tools it can use,
outputs special syntax requesting one — JSON, XML or `tool_name(arguments)`, which he says does not
matter — and stops; the caller's code parses that output, runs the tool and starts a new prompt with
the result. By then, according to that post, it worked with almost every model, most of which were
specifically trained for tool use, and there were leaderboards such as the Berkeley Function-Calling
Leaderboard tracking which models did it best. He writes that all the big model vendors — OpenAI,
Anthropic, Google, Mistral and Meta — have a version of it built into their APIs, called either tool
usage or function calling, and that it is the same underlying pattern; that local runtimes had it
too, with Ollama having added tool support and the llama.cpp server supporting it; and that a year
earlier he had not felt vendor support was mature enough to design an abstraction over it, whereas
there was now a very definite consensus among vendors on how it should work. He built that
abstraction into his own [[SoftwareApplication/llm]] tool.

## Related Terms

- [[DefinedTerm/tool-use-design-pattern]]
- [[DefinedTerm/agentic-tool-use]]
- [[DefinedTerm/tool-namespacing]]
- [[DefinedTerm/tool-search]]
- [[DefinedTerm/programmatic-tool-calling]]
- [[DefinedTerm/client-and-server-tools]]
- [[DefinedTerm/react-prompting]] — the pattern one early commentator described function calling as implementing
