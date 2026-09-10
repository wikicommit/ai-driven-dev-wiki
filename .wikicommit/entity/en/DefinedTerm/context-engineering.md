---
title: "Context engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agents, context-window, llm, prompting]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "The set of strategies for curating and maintaining the optimal set of tokens available to a language model during inference, presented by Anthropic as the natural progression of prompt engineering."
---

Context engineering is the set of strategies for curating and maintaining the optimal set of
tokens — the information available to a large language model during inference — so that the
model's holistic state at any given moment is the one most likely to yield the desired
behaviour. Anthropic frames it as the natural progression of
[[DefinedTerm/prompt-engineering]]: where prompt engineering asks how to write effective
instructions, context engineering asks what configuration of the entire context — system
instructions, tools, external data, message history and everything else that lands there — is
most likely to generate a model's desired behaviour. Its guiding principle is to find the
smallest possible set of high-signal tokens that maximise the likelihood of a desired outcome.

## Usage
The term applies to agents that operate over multiple turns of inference and longer time
horizons. An agent running in a loop generates more and more data that could be relevant to the
next turn, and that information has to be cyclically refined; context engineering is the
curation of what will go into a limited context window from that constantly evolving universe of
possible information. Anthropic describes the discipline as iterative rather than discrete — the
curation step recurs every time something is passed to the model, in contrast to the one-off act
of writing a prompt — and set out its own account of the practice in
[[BlogPosting/effective-context-engineering-for-ai-agents]].

Across the components of context, Anthropic's guidance is to keep everything informative yet
tight:

- **System prompts** should be extremely clear, use simple and direct language, and present
  ideas at the right altitude — specific enough to guide behaviour effectively, yet flexible
  enough to leave the model strong heuristics. Anthropic recommends organising prompts into
  distinct sections delineated with XML tagging or Markdown headers, while noting that exact
  formatting is likely becoming less important as models grow more capable.
- **Tools** define the contract between an agent and its information and action space, so they
  should return token-efficient information and encourage efficient agent behaviour. Anthropic
  describes well-designed tools as self-contained, robust to error and extremely clear about
  their intended use, with descriptive and unambiguous input parameters.
- **Examples**, or few-shot prompting, should be a curated set of diverse, canonical cases that
  portray the expected behaviour of the agent rather than an exhaustive list of edge cases.

## When It Applies
- Applies once an agent operates over multiple turns, where the whole context state rather than
  the prompt alone determines behaviour. Anthropic notes that in the early days of building with
  LLMs, prompting was the biggest component of the work, because most use cases outside everyday
  chat were one-shot classification or text generation.
- Assumes context is a finite resource with diminishing marginal returns. The practice rests on
  [[DefinedTerm/context-rot]] and on the [[DefinedTerm/attention-budget]] framing rather than on
  any particular context-window size; Anthropic argues that waiting for larger windows is not a
  substitute, since windows of all sizes remain subject to context pollution and
  information-relevance concerns where the strongest agent performance is wanted.
- Misapplied when engineers hardcode complex, brittle logic into prompts, when they instead give
  vague high-level guidance that falsely assumes shared context, when a tool set grows bloated
  enough that a human engineer could not say which tool applies in a given situation, or when a
  laundry list of edge cases is stuffed into a prompt in place of canonical examples. Anthropic's
  stated remedy is to start from a minimal prompt on the best available model and add
  instructions and examples in response to failure modes found in testing.
- Presented as Anthropic's own working view, drawn from building agents and working alongside its
  customers, rather than as a measured result. Anthropic observes that smarter models require
  less prescriptive engineering, and gives "do the simplest thing that works" as its standing
  advice for teams building agents on Claude.

## Related Terms
- [[DefinedTerm/prompt-engineering]]
- [[DefinedTerm/context-rot]]
- [[DefinedTerm/attention-budget]]
- [[DefinedTerm/just-in-time-context-retrieval]]
- [[DefinedTerm/compaction]]
- [[DefinedTerm/structured-note-taking]]
- [[DefinedTerm/sub-agent-architecture]]
