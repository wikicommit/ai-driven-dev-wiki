---
title: "Attention budget"
type: "schema:DefinedTerm"
lang: en
tags: [agents, context-window, llm]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "Anthropic's framing of a language model's capacity to attend to its context as a finite pool that every additional token depletes."
---

The attention budget is Anthropic's framing of a language model's capacity to attend to its
context as a finite pool that every additional token depletes. Drawing an analogy to the limited
working memory capacity of humans, Anthropic argues that LLMs draw on such a budget when parsing
large volumes of context, so each new token introduced increases the need to carefully curate
what the model is given.

## Usage
Anthropic traces this attention scarcity to architectural constraints. Transformer-based models
let every token attend to every other token across the entire context, which yields n² pairwise
relationships for n tokens; as context length increases, a model's ability to capture those
relationships is stretched thin, creating a natural tension between context size and attention
focus. Two further factors compound it. Models develop their attention patterns from training
data distributions in which shorter sequences are typically more common than longer ones, leaving
them with less experience and fewer specialised parameters for context-wide dependencies. And
techniques such as position encoding interpolation, which let models handle longer sequences by
adapting them to the originally trained smaller context, cost some accuracy in token-position
understanding.

Anthropic presents these factors together as producing a performance gradient rather than a hard
cliff, and treats the budget as the reason good [[DefinedTerm/context-engineering]] means finding
the smallest possible set of high-signal tokens that maximise the likelihood of a desired
outcome.

## Related Terms
- [[DefinedTerm/context-rot]]
- [[DefinedTerm/context-engineering]]
