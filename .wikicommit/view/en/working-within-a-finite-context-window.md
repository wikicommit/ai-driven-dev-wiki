---
title: "Working within a finite context window"
lang: en
kind: landscape
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"
derived_from:
  - path: .wikicommit/entity/en/DefinedTerm/context-engineering.md
    source_commit: 0f0c396e9523013274367f735327608adbca5281
  - path: .wikicommit/entity/en/DefinedTerm/prompt-engineering.md
    source_commit: 0f0c396e9523013274367f735327608adbca5281
  - path: .wikicommit/entity/en/DefinedTerm/context-rot.md
    source_commit: 0f0c396e9523013274367f735327608adbca5281
  - path: .wikicommit/entity/en/DefinedTerm/attention-budget.md
    source_commit: 0f0c396e9523013274367f735327608adbca5281
  - path: .wikicommit/entity/en/DefinedTerm/compaction.md
    source_commit: 0f0c396e9523013274367f735327608adbca5281
  - path: .wikicommit/entity/en/DefinedTerm/structured-note-taking.md
    source_commit: 0f0c396e9523013274367f735327608adbca5281
  - path: .wikicommit/entity/en/DefinedTerm/sub-agent-architecture.md
    source_commit: 0f0c396e9523013274367f735327608adbca5281
  - path: .wikicommit/entity/en/BlogPosting/effective-context-engineering-for-ai-agents.md
    source_commit: 0f0c396e9523013274367f735327608adbca5281
  - path: .wikicommit/entity/en/SoftwareApplication/context-engineering-kit.md
    source_commit: 0f0c396e9523013274367f735327608adbca5281
  - path: .wikicommit/entity/en/Organization/anthropic.md
    source_commit: 0f0c396e9523013274367f735327608adbca5281
---

The pages this wiki holds on agents and their context share one premise: that the context
available to a language model during inference is a finite resource with diminishing marginal
returns, rather than a container to be filled. This page is a way into that group — where the
area starts, why the constraint is held to exist, what is done about it when a task outruns the
window, and where the account it rests on comes from.

## Where the area starts
[[DefinedTerm/context-engineering]] is the entry point. It names the set of strategies for
curating and maintaining the optimal set of tokens available to a model during inference, and its
guiding principle — find the smallest possible set of high-signal tokens that maximise the
likelihood of a desired outcome — is what the rest of the area keeps returning to. It is framed
as the natural progression of [[DefinedTerm/prompt-engineering]], and as encompassing it rather
than replacing it: prompt writing becomes one component of managing a whole context state that
also holds tools, external data and message history.

The dividing line between the two is where the relevant state can be settled. Prompt engineering
assumes it can be settled in advance, in writing, which holds for one-shot classification and
text generation. Context engineering takes over once an agent operates over multiple turns, where
information accumulates during the run and has to be cyclically refined.

## Why the constraint is held to exist
The reasoning behind the premise is carried by [[DefinedTerm/context-rot]] and
[[DefinedTerm/attention-budget]], which answer different questions. Context rot is the empirical
side: recall accuracy declines as the number of tokens in the context window grows, attributed to
needle-in-a-haystack style benchmarking and reported as emerging across all models, though some
degrade more gently than others. The attention budget is the mechanical side: transformer
attention creates n² pairwise relationships for n tokens, training distributions favour shorter
sequences, and techniques for extending context length cost some token-position accuracy.

Both pages describe the result as a performance gradient rather than a hard cliff, and both are
used to argue that larger context windows are not the way out — windows of all sizes are held to
remain subject to context pollution and information-relevance concerns wherever the strongest
agent performance is wanted.

## What is done when a task outruns the window
The techniques recorded here are presented as suiting different task shapes rather than as
ranked alternatives:

- [[DefinedTerm/compaction]] summarises a conversation nearing the window limit and reinitiates a
  new window with that summary — recommended for work requiring extensive back-and-forth, and
  described as typically the first lever.
- [[DefinedTerm/structured-note-taking]] has the agent write notes that persist outside the
  window and are read back in later — recommended for iterative development with clear
  milestones.
- [[DefinedTerm/sub-agent-architecture]] gives focused tasks to sub-agents with clean windows
  while a main agent coordinates from a high-level plan, each sub-agent returning a distilled
  summary rather than its working context — recommended for complex research where parallel
  exploration pays dividends.

Alongside them sits a change in how data reaches the window at all:
[[DefinedTerm/just-in-time-context-retrieval]], in which an agent holds lightweight identifiers
and loads the underlying data at runtime, often as a hybrid with up-front retrieval.

## Where the account comes from
Most of this area traces to a single document,
[[BlogPosting/effective-context-engineering-for-ai-agents]], written by
[[Organization/anthropic]]'s Applied AI team, with [[SoftwareApplication/claude-code]] as its
worked example throughout. That matters for how the pages read: the post takes its examples from
Anthropic's own products and is explicit that its guidance comes from what the team has observed
rather than from controlled results. Several of its claims lean on earlier writing it links to
instead of restating, so the backing for those points is not set out in the post itself.

The pages recording the techniques carry that provenance forward, and they do not all rest on the
same kind of evidence: compaction is established as Anthropic's own implemented practice in
Claude Code and as a shipped platform feature, structured note-taking rests partly on a
demonstration Anthropic reports rather than a controlled measurement, and the sub-agent
architecture's reported improvement over single-agent systems is a comparison whose basis is not
stated alongside the claim.

## Where the area extends past that account
[[SoftwareApplication/context-engineering-kit]] approaches the same subject from a different
direction: it packages context-engineering patterns as installable plugins for coding agents,
built from prompts its own developers use daily and from plugins derived from benchmarked papers.
Its reliability-versus-token-cost comparison is its own, based on its team's development usage
rather than on an independent benchmark. It is also where this area meets the wiki's pages on
agent workflows: the kit ships plugins implementing the methodologies described in
[[DefinedTerm/spec-driven-development]] and [[DefinedTerm/subagent-driven-development]], and the
[[DefinedTerm/first-principles-framework]] is among the plugins it distributes.
