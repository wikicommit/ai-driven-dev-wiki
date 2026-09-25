---
title: "Tool Use Examples"
type: "schema:DefinedTerm"
lang: en
tags: [tool-use, agent-tooling]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/advanced-tool-use'
    hash: sha256:37cff587dcd276ffbe27f31fcfa6f7985ccacfd5d06270baf40025725a068a97
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Claude Developer Platform feature for including sample tool calls directly in a tool definition, so that a model learns usage patterns — formats, ID conventions, nested-structure usage and which optional parameters go together — that a JSON schema can declare as valid but cannot express."
---

Tool Use Examples is the name [[Organization/anthropic]] gives to a feature of the Claude Developer
Platform that lets a developer attach sample tool calls to a tool definition, in an `input_examples`
field alongside the input schema. Its premise is that JSON Schema defines structure — types, required
fields, allowed values — but cannot express usage patterns: which format a date field should take,
what an identifier looks like, when to populate a nested object, or how one parameter relates to
another. The examples show those patterns concretely, so that the model can infer them rather than
guess, with the aim of reducing malformed tool calls and inconsistent parameter use.

## Usage

The feature was introduced in [[BlogPosting/introducing-advanced-tool-use]] as one of three beta
features for agents working with large tool libraries, alongside the Tool Search Tool
([[DefinedTerm/tool-search]]) and [[DefinedTerm/programmatic-tool-calling]], and is positioned as
the answer to the third of their bottlenecks: parameter errors and malformed calls. The announcement
illustrates it with a support-ticket tool whose three examples — a fully specified critical bug, a
feature request with a reporter but no contact or escalation details, and a task with only a title —
are meant to teach date and ID formats, how to build the nested reporter object, and which optional
parameters appear together at each level of priority.

## When It Applies

Anthropic describes the examples as most useful for complex nested structures where valid JSON does
not imply correct usage, tools with many optional parameters whose inclusion matters, APIs with
domain-specific conventions not captured in the schema, and similar tools that examples help tell
apart. It describes them as less useful for simple single-parameter tools, standard formats such as
URLs or email addresses that the model already understands, and validation that JSON Schema
constraints handle better. Because examples add tokens to every tool definition, the stated
trade-off is whether the accuracy gain outweighs that cost.

Its guidance on writing them is to use realistic data rather than placeholder values, to show
variety across minimal, partial and full specifications, to keep to one to five examples per tool,
and to add examples only where correct usage is not obvious from the schema. The evidence behind the
feature is Anthropic's own: the announcement reports that in internal testing, tool use examples
improved accuracy on complex parameter handling from 72% to 90%.

## Related Terms

- [[DefinedTerm/tool-search]]
- [[DefinedTerm/programmatic-tool-calling]]
- [[DefinedTerm/function-calling]]
- [[DefinedTerm/agentic-tool-use]]
