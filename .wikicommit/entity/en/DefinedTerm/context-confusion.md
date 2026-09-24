---
title: "Context confusion"
type: "schema:DefinedTerm"
lang: en
tags: [context-window, llm, agents]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/60229/'
    hash: sha256:10d03ac2a5d00b558656acc685e174052e16d06256b8fd88f86df9be1d954d01
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A state in which excessive information, overly abstract instructions, or contradictory instructions leave an LLM unable to judge which information to prioritize, making its output unstable."
---

Context confusion is the state in which excessive information, overly abstract instructions, or instructions that contradict one another leave a language model unable to judge which information to prioritize. [[BlogPosting/spec-driven-development-context-engineering-custom-slash-commands]] names it as one of three problems that [[DefinedTerm/context-engineering]] is meant to address, alongside [[DefinedTerm/context-rot]] and [[DefinedTerm/context-poisoning]]. Its symptoms, as that post describes them, are results that vary widely from one run to the next and a greater tendency to hallucinate.

## Usage

The post explains the cause in terms of the [[DefinedTerm/signal-to-noise-ratio]] of the context: when the information the task actually needs (signal) makes up a smaller share relative to unrelated information and redundant logs (noise), the model's attention weighting stops working properly, so important information is under-weighted and unimportant information over-weighted, and output quality becomes unstable.

Its worked example comes from designing [[DefinedTerm/custom-slash-commands]]: a single command that chained web research, document creation, guideline checking and correction was pulled off course by the large amount of noise from web search, which the author identifies as causing context confusion and context rot. The remedy the post proposes is to split such work into commands with a single responsibility each and to inject only the minimum information a task needs.

## Related Terms

- [[DefinedTerm/context-rot]]
- [[DefinedTerm/context-poisoning]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/signal-to-noise-ratio]]
