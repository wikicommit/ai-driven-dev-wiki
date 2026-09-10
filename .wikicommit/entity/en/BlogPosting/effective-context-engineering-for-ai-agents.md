---
title: "Effective context engineering for AI agents"
type: "schema:BlogPosting"
lang: en
tags: [agents, anthropic, context-window, prompting]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "Anthropic's Applied AI team on treating context as a finite resource: the anatomy of effective context, just-in-time retrieval, and three techniques for long-horizon tasks."
  author: ["Prithvi Rajasekaran", "Ethan Dixon", "Carly Ryan", "Jeremy Hadfield"]
  datePublished: "2025-09-29"
  publisher: "[[Organization/anthropic]]"
---

This post argues that building with language models is becoming less about finding the right words
and phrases for a prompt and more about answering a broader question: what configuration of
context is most likely to generate a model's desired behaviour. It names that practice
[[DefinedTerm/context-engineering]] and positions it as the natural progression of
[[DefinedTerm/prompt-engineering]] — where prompting concerns the instructions given to a model,
context engineering concerns the whole set of tokens present during inference, system
instructions, tools, external data and message history alike.

Its central claim is that context is a finite resource with diminishing marginal returns. The post
cites needle-in-a-haystack style benchmarking for [[DefinedTerm/context-rot]] and offers the
[[DefinedTerm/attention-budget]] as a framing for why: transformer attention creates n² pairwise
relationships for n tokens, training distributions favour shorter sequences, and techniques for
extending context length cost some precision. From this it derives a guiding principle — find the
smallest possible set of high-signal tokens that maximise the likelihood of a desired outcome —
and works through what that means for system prompts, tools and examples.

The second half turns to retrieval and to tasks that outrun the context window. It describes the
field moving from embedding-based pre-inference retrieval toward
[[DefinedTerm/just-in-time-context-retrieval]], often as a hybrid of the two, and sets out three
techniques for long-horizon work: [[DefinedTerm/compaction]],
[[DefinedTerm/structured-note-taking]] and [[DefinedTerm/sub-agent-architecture]]. Throughout,
[[SoftwareApplication/claude-code]] serves as the worked example.

## Key Points
- Context engineering is the set of strategies for curating and maintaining the optimal set of
  tokens during LLM inference, and is the natural progression of prompt engineering. This is
  [[Organization/anthropic]]'s own framing of how the two terms relate.
- Context rot — recall accuracy falling as the number of tokens in the context window grows —
  emerges across all models, though some degrade more gently than others. The post attributes this
  to studies on needle-in-a-haystack style benchmarking.
- LLMs have a finite attention budget, which the post traces to transformer attention's n² pairwise
  relationships, to training distributions in which shorter sequences dominate, and to the
  token-position accuracy cost of position encoding interpolation. It describes the result as a
  performance gradient rather than a hard cliff.
- Good context engineering means finding the smallest possible set of high-signal tokens that
  maximise the likelihood of a desired outcome.
- System prompts should sit at the right altitude — between brittle hardcoded if-else logic and
  vague guidance that falsely assumes shared context. This is the post's own recommendation, based
  on the two failure modes Anthropic reports seeing in practice.
- Bloated tool sets that cover too much functionality, or that create ambiguous decision points,
  are among the most common failure modes Anthropic reports: if a human engineer cannot
  definitively say which tool should be used in a given situation, an agent cannot be expected to
  do better.
- Few-shot examples should be a curated set of diverse, canonical cases rather than a laundry list
  of edge cases stuffed into a prompt.
- The post adopts a simple definition of agents — LLMs autonomously using tools in a loop — which
  it says it has gravitated toward, crediting a formulation from outside Anthropic.
- Just-in-time context retrieval, in which an agent holds lightweight identifiers and loads data
  at runtime, is where the post sees engineering practice heading, with a hybrid of up-front and
  runtime retrieval often the most effective arrangement. The evidence offered is Anthropic's own
  product experience and what it observes among its customers.
- Larger context windows are not expected to remove the problem: the post argues that for the
  foreseeable future, windows of all sizes remain subject to context pollution and
  information-relevance concerns where the strongest agent performance is wanted.
- Compaction, structured note-taking and sub-agent architectures suit different task shapes —
  respectively extensive back-and-forth, iterative development with clear milestones, and complex
  research where parallel exploration pays dividends.
- Smarter models require less prescriptive engineering, so the post expects agentic design to trend
  toward progressively less human curation. Its standing advice remains "do the simplest thing
  that works".

## Context
The post is written by Anthropic's Applied AI team and takes its examples from Anthropic's own
products, so its recommendations rest largely on that team's engineering experience and on what it
reports observing while working alongside customers, rather than on measured comparisons. It
presents itself as offering a refined mental model for building steerable, effective agents rather
than a set of benchmarks, and it is explicit that its guidance comes from what the team has
observed rather than from controlled results. Several of its claims lean on earlier writing that it
links to instead of restating — on context rot, on tool design, on its own multi-agent work, and on
the definition of agents it adopts — so the backing for those particular points is not set out in
the post itself.
