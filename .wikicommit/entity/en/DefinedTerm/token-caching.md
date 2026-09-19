---
title: "Token Caching"
type: "schema:DefinedTerm"
lang: en
tags: [llm-internals, coding-agents, cost]
sources:
  - type: url
    url: 'https://simonwillison.net/guides/agentic-engineering-patterns/how-coding-agents-work/'
    hash: sha256:a8be3f0926e2b75d77e83036446bf575cf49b7dff42641018af0909da9d387eb
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A cheaper provider rate for input tokens whose prefix has already been processed recently, because the expensive calculations behind that prefix can be cached and reused. It is why coding agents are built to append to a conversation rather than revise its earlier parts."
---

Token caching is the practice, offered by most model providers, of charging a cheaper rate for
**cached input tokens** — common token prefixes that have already been processed within a short time
period — because the underlying infrastructure can cache and reuse many of the expensive calculations
that produced them. As the source describes it, it is a matter of what an unchanged prefix is charged
at rather than of what the model can do.

## Usage

Its relevance to coding agents follows from how [[DefinedTerm/chat-templated-prompt]] works. Models
are stateless, so the software around them replays the whole conversation on every turn, and the
input grows as the session lengthens. Token caching offsets part of that growth — but only for the
prefix that has not changed. The design consequence is stated directly in the source: coding agents
are built with this optimization in mind and **avoid modifying earlier conversation content**, so
that the cache is used as efficiently as possible.

That constraint is worth noting because it is a design pressure the source states outright while
saying nothing about how it is resolved: efficient cache use and rewriting earlier conversation
content pull against each other, and the agents the source describes resolve it by not rewriting.

## Related Terms

[[DefinedTerm/chat-templated-prompt]], [[DefinedTerm/compaction]], [[DefinedTerm/context-rot]],
[[DefinedTerm/context-engineering]], [[DefinedTerm/ai-coding-agent]]
