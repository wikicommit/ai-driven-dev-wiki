---
title: "Gemini API"
type: "schema:SoftwareApplication"
lang: en
tags: [tool-use, llm, agent-tooling]
sources:
  - type: url
    url: 'https://ai.google.dev/gemini-api/docs/tools'
    hash: sha256:56f15bec50e7429858d3e245833b8767f93534d45e9f989d56c4ec97baaa3a96
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Google's hosted API for its Gemini models. It offers a suite of fully managed built-in tools that run on Google's servers, alongside custom tools the calling application defines and executes through function calling."
  applicationCategory: "Hosted model API"
  featureList: "Built-in tools (Google Search, Google Maps, Code Execution, URL Context, Computer Use in preview, File Search); custom tools via function calling; combining built-in and custom tools in one turn (preview); structured outputs, combinable with built-in tools for Gemini 3 series models; tool use in real-time streaming sessions through the Live API"
  author: "[[Organization/google]]"
---

The Gemini API is [[Organization/google]]'s hosted interface to its Gemini models. Its
documentation on tools describes them as specific capabilities — such as Google Search or code
execution — that a model can use to answer queries, and presents them as what lets Gemini models
take action in the world, access real-time information and perform complex computational tasks.
Tools can be used both in standard request-response interactions and in real-time streaming
sessions through the API's Live API.

The API offers two kinds of tool: a suite of fully managed, built-in tools, and custom tools that
the developer defines using function calling. For multi-step, goal-oriented systems the
documentation points to a separate agents overview rather than to the tools themselves.

## Capabilities

The built-in tools are listed as follows, each with the use it is intended for:

- **Google Search** — grounding responses in current events and facts from the web, with the stated
  aim of reducing hallucinations.
- **Google Maps** — building location-aware assistants that find places, give directions and
  provide local context.
- **Code Execution** — letting the model write and run Python code to solve maths problems or
  process data accurately.
- **URL Context** — directing the model to read and analyse content from specific web pages or
  documents.
- **Computer Use** (preview) — letting Gemini view a screen and generate actions that interact with
  web browser interfaces, executed on the client side (see [[DefinedTerm/computer-use]]).
- **File Search** — indexing and searching the developer's own documents to enable
  retrieval-augmented generation.

How a tool call is executed depends on which kind it is — the split described under
[[DefinedTerm/client-and-server-tools]]. For the built-in tools other than Computer Use, the whole
process happens within one API call: Gemini decides it needs a tool, executes it on Google's
servers — the documentation's example searches for a stock price and then runs Python to take its
square root — and returns a final answer grounded in the results. For custom tools and for Computer
Use, the application handles execution: Gemini may return structured JSON calling a specific
function, always carrying a unique `id`; the application runs the function and sends the result back
with the same `id`; and Gemini uses it to produce a final response or another tool call. A separate
preview endpoint, `gemini-3.1-pro-preview-customtools`, is offered for developers building with a
mix of bash and custom tools.

As a preview feature, Gemini 3 series models can combine built-in and custom tools in a single turn,
which the documentation calls tool context circulation. The developer enables a combination flag
alongside the declared tools; Gemini executes built-in tools and yields to the application when it
generates a client-side function call, returning the tool-call confirmation, the built-in tool's
results, the JSON for the custom call and encrypted thought signatures that preserve context. The
application then returns all parts of that response together with its own function results, and
Gemini generates the final answer from the combined context.

The documentation separates function calling from structured outputs by purpose: function calling is
for when the model needs to perform an intermediate step by connecting to the developer's own tools
or data systems, while structured outputs are for when the model's final response must strictly
follow a specific schema, for example to render a custom interface. For Gemini 3 series models, as a
preview feature, structured outputs can be combined with built-in tools so that responses grounded in
external data or computation still adhere to a strict schema.

## Adoption & Ecosystem

The tools documentation links onward to guides for each built-in tool, to a function calling guide
and to a tool combination guide, and notes that some tools carry costs of their own set out on the
API's pricing page.
