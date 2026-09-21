---
title: "Context engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agents, context-window, llm, prompting]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
  - type: url
    url: 'https://aws.amazon.com/cn/blogs/china/agentic-ai-infrastructure-practice-series-nine-context-engineering/'
    hash: sha256:1ea97ed3d4e23cb29114ffee329716c05e979b914a7a52d5b181bf258202267f
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The practice of curating and dynamically managing what information enters a language model's context window during inference. Two vendor accounts of it coexist in this wiki's sources: one framing it as the natural progression of prompt engineering, the other stressing a fundamental difference from it and presenting context engineering as addressing its limitations."
---

Context engineering is the practice of curating and dynamically managing what information
occupies a large language model's context window during inference. Two of this wiki's sources
define the term, each in its own words and each writing about its own practice. They agree on
the problem and on the substantive contrast — a static written prompt against a dynamically
assembled context — and differ in emphasis on how the term stands to prompt engineering, and in
what kind of thing they say it is.

Anthropic — writing as a model provider rather than a cloud vendor — defines it as the set of
strategies for curating and maintaining the optimal set of tokens available during inference,
considering the holistic state available to the model at any given time and what behaviours
that state might yield. It frames the practice as the natural progression of
[[DefinedTerm/prompt-engineering]]: where prompt engineering asks how to write effective
instructions, context engineering asks what configuration of the entire context — system
instructions, tools, external data, message history and everything else that lands there — is
most likely to generate a model's desired behaviour. Its guiding principle is to find the
smallest possible set of high-signal tokens that maximise the likelihood of a desired outcome.

AWS, in [[BlogPosting/agentic-ai-infrastructure-context-engineering]], relays a definition it
presents as an understanding the industry has converged on: a technical framework for optimizing
a model's reasoning and decision-making by dynamically managing the information entering its
context window, whose stated aims are to fill the window precisely and to cut cost. Where
Anthropic says progression, this account stresses a fundamental difference from traditional
prompt engineering and presents context engineering as addressing its limitations — a static
string cannot carry dynamic multi-source information such as real-time data, historical state or
tool interfaces, so context is instead treated as a collection of dynamic structured components
managed through explicit memory and modular composition. It does not treat the two as unrelated:
its own context-retrieval-and-generation component lists prompt engineering as one of the three
techniques inside it.

What separates them is less the contrast each draws than what each says the thing is.
Anthropic's is a set of strategies; AWS's is a technical framework organized around a
retrieval–processing–management lifecycle with cost reduction among its stated aims, which
Anthropic's account does not organize that way. Neither post engages the other's framing, though
AWS's does build throughout on Anthropic's models.

## Usage
The term applies to agents that operate over multiple turns of inference and longer time
horizons. Anthropic describes an agent running in a loop as generating more and more data that
could be relevant to the next turn, information that must then be cyclically refined, and
context engineering as the curation of what goes into the limited context window from that
constantly evolving universe of possible information. It describes the discipline as iterative
rather than discrete — the
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

AWS decomposes the same territory structurally rather than by advice. It describes context as
made of input (system instructions, external knowledge retrieval, tool definitions, global state
and user input), memory (long-term and short-term), and output (tool execution results and
model-generated structured content); and it names three core components that form an iterative
loop — context retrieval and generation, context processing, and context management, the last
acting as the hub that organizes, compresses and schedules information across the whole flow. It
also names a "context optimizer" for this work, stating that today it is mainly an engineering
implementation and that a possible future evolution is a model-driven optimizer — one that would
decide, from the current user input, the task goal and the model's state, whether to compress,
which compression strategy to use, what to discard, what to store as memory, and when to backfill
memory.

## When It Applies
- Applies once an agent operates over multiple turns, where the whole context state rather than
  the prompt alone determines behaviour. Anthropic notes that in the early days of building with
  LLMs, prompting was the biggest component of the work, because most use cases outside everyday
  chat were one-shot classification or text generation.
- Assumes context is a finite resource with diminishing marginal returns. The practice rests on
  [[DefinedTerm/context-rot]] and on the [[DefinedTerm/attention-budget]] framing rather than on
  any particular context-window size; Anthropic argues that waiting for larger windows is not a
  substitute, since windows of all sizes remain subject to context pollution and
  information-relevance concerns where the strongest agent performance is wanted. AWS puts a number on the
  growth that creates the pressure rather than on the returns: it counts a single agent task
  decomposed into ten subtasks, each taking two tool calls, as producing 41 new context records,
  and notes that in a multi-agent system each agent carries that load and the total multiplies
  again.
- Misapplied when engineers hardcode complex, brittle logic into prompts, when they instead give
  vague high-level guidance that falsely assumes shared context, when a tool set grows bloated
  enough that a human engineer could not say which tool applies in a given situation, or when a
  laundry list of edge cases is stuffed into a prompt in place of canonical examples. Anthropic's
  stated remedy is to start from a minimal prompt on the best available model and add
  instructions and examples in response to failure modes found in testing.
- Neither account is an independent evaluation; each vendor is writing about its own practice.
  Anthropic's is drawn from building agents and working alongside its customers; it observes that
  smarter models require less prescriptive engineering, and gives "do the simplest thing that
  works" as its standing advice for teams building agents on Claude. AWS's is drawn from its own
  product stack and does put numbers behind one part of it — for Amazon Bedrock's prompt cache
  specifically, cached tokens priced 90% below standard input tokens, and a claim that in stable
  agent workflows cache hit rates *can* exceed 90% and overall inference cost *can* fall by 80%.
  These are vendor-reported figures about one product, stated as what is achievable and without a
  methodology or head-to-head baseline, not measurements of context engineering in general.

## Related Terms
- [[DefinedTerm/prompt-engineering]]
- [[DefinedTerm/context-rot]]
- [[DefinedTerm/attention-budget]]
- [[DefinedTerm/just-in-time-context-retrieval]]
- [[DefinedTerm/compaction]]
- [[DefinedTerm/structured-note-taking]]
- [[DefinedTerm/sub-agent-architecture]]
