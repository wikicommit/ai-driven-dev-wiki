---
title: "Agentic Design Pattern #1: Tool Calling"
type: "schema:BlogPosting"
lang: en
tags: [agents, tool-use, agent-architecture]
sources:
  - type: url
    url: 'https://blog.dagworks.io/p/agentic-design-pattern-1-tool-calling'
    hash: sha256:f5276fdca09410e46b0e304c27f4f41294afee574a8aae025568b5534898ad22
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The opening post of DAGWorks's agentic design patterns series, which argues that \"tool\" and \"function\" are synonyms, separates both from structured outputs, and works through a tool-calling agent built with the Burr state-machine library."
  author: ["Elijah ben Izzy"]
  datePublished: "2024-09-28"
  publisher: "DAGWorks Inc."
---

"Agentic Design Pattern #1: Tool Calling" opens a series in which DAGWorks sets out the patterns it has seen make agents reliable in production, and shows each one implemented with [[SoftwareApplication/burr]], its own Python state-machine library. The post's stated motivation is an influx of Burr users wanting help modelling their systems, who after building a chatbot inevitably migrate toward building agents, and the observation that although agents are treated as new and chaotic, a few common patterns have emerged. It offers a working definition to go on with: an agent is anything that uses the output of an LLM to do something on a user's behalf, rather than just parroting it back.

Much of the post is spent on vocabulary before any code appears, because the author judges the distinction between "tool", "function" and "structured output" to be made more complex than it is. Its answer is blunt — a tool and a function are synonyms — and the rest is a walkthrough of the [[DefinedTerm/tool-use-design-pattern]] in that vocabulary: define functions, describe them to the model, let the model pick one and supply its arguments, execute it, and format the result. The concluding section argues the case for orchestrating this with Burr rather than writing the API calls directly, on grounds of graph readability, observability and production concerns.

## Key Points

- Defines an agent as anything that uses the output of an LLM to do something on a user's behalf, rather than just returning the model's text to the user.
- Argues that "tool" and "function" are synonyms: a tool maps to the software-engineering concept of a function, because for an agent built in code the simplest way to act on a user's behalf is to call one, and "tool" is simply the higher-level word for what an agent can do. The post attributes the phrase "tool call" to a merging of "function call" and "tool use".
- Observes that the industry has yet to align on the terminology, with major model providers naming the same feature differently in their own APIs and documentation.
- Distinguishes structured outputs from tool calling: what comes back when a model picks a tool is a JSON representation of the tool's name and its arguments, and that JSON-producing behaviour can be co-opted to get a fully structured response with no actual tool behind it, which the post presents as a way to generalize outside any specific tool-calling API.
- Frames the core reframing the pattern requires: current models are largely closed off from the internet, so rather than asking a model what the weather is, the developer asks it how to determine the weather given that X, Y and Z can be done — the model's strength being to determine intent and say what to do, not to execute it.
- Describes implementing the pattern as a thin layer over any provider API that supports tool calling, though the worked example assumes OpenAI throughout: Python's `inspect` module reads function signatures and formats them into the OpenAI-compatible type, so adding a new tool means adding a function.
- Recommends a fallback tool that lets the model answer from its own knowledge, on the reasoning that not every question needs a tool.
- Argues for modelling one action per tool rather than a single dispatching action, specifically so that every available tool appears in the application graph.
- Reports that the model was unreliable at choosing a tool — sometimes declining to choose one, sometimes losing track of the instructions — and that reasonable behaviour was reached through prompt engineering iterated on in the library's UI.

## Notes

The post is the vendor's own writing about its own library, and it says so plainly: the argument in its closing sections is that Burr's orchestration and observability are worth the dependency, and the example is acknowledged as a toy application. Its forward-looking section names four further patterns the series intends to cover — chaining tools together to answer a question, querying and calling a set of tools in parallel, using multiple agents on one question, and having agents work together constructively — none of which this post addresses.

The code itself is not reproduced in the extracted text: the post presents its examples as screenshots with links out to gists and a repository example directory, so what is recorded above is the design argument rather than the implementation.
