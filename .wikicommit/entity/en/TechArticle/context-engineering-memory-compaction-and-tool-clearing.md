---
title: "Context engineering: memory, compaction, and tool clearing"
type: "schema:TechArticle"
lang: en
tags: [context-engineering, context-window, long-horizon-tasks, memory]
sources:
  - type: url
    url: 'https://platform.claude.com/cookbook/tool-use-context-engineering-context-engineering-tools'
    hash: sha256:ff18c6ce4f289fc1d0603542473d89de2170efe173360a83c70d460ec9204888
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Claude Cookbook notebook, published in March 2026, that compares three context-engineering primitives for long-running agents — compaction, tool-result clearing and the memory tool — explaining what each operates on, what it trades away, and when to use, combine or skip them."
  author: ["Isabella He"]
  publisher: "[[Organization/anthropic]]"
  datePublished: "2026-03-20"
  dependencies: "Python 3.11+ with the anthropic, python-dotenv and matplotlib packages; an Anthropic API key; the research_corpus.py file shipped alongside the notebook"
---

This notebook in Anthropic's Claude Cookbook is a hands-on comparison of three strategies for
managing the context of long-horizon agents: [[DefinedTerm/compaction]],
[[DefinedTerm/tool-result-clearing]], and memory, which it describes as structured note-taking
(see [[DefinedTerm/structured-note-taking]]). It starts from the observation that tool results, the
model's reasoning and user messages all accumulate until an agent either hits its token limit or pays
for context that no longer helps, and it cites [[DefinedTerm/context-rot]] — declining recall as the
context grows — as a reason the problem bites even before the hard limit. Following Anthropic's
framing of [[DefinedTerm/context-engineering]] as a resource problem, it sets out to show how the
three primitives differ, since all three make the window more efficient and are easy to confuse.

The worked example is a long-running research agent that reads eight synthetic review documents of
roughly 40K tokens each (about 320K tokens in total) in two batches, takes notes, and writes a
comparative synthesis across more than one session. The notebook argues that this workload naturally
hits all three problems at once: bulky document reads, a long analytical dialogue, and knowledge that
must survive between sessions. Each primitive is shown first as a minimal hand-written implementation
and then through Anthropic's first-party API feature, and all three are finally run together.

## Details

- **What each primitive operates on.** Compaction is a whole-transcript operation that replaces the
  conversation with a model-written summary; tool-result clearing is a sub-transcript operation that
  replaces old tool results with a placeholder while keeping the record of the call; memory moves
  information out of the window into storage the agent reads back later. The notebook's rough mental
  model is that compaction compresses the whole window, clearing drops stale re-fetchable data inside
  it, and memory lets information survive across sessions.
- **API features and knobs.** It maps the three to Anthropic API features: compaction as the
  `compact_20260112` context edit (server-side, triggered at a token threshold with a minimum of 50K and
  a default of 150K, configurable with custom `instructions` and `pause_after_compaction`); clearing as
  the `clear_tool_uses_20250919` context edit (default trigger 100K, default `keep` of three tool uses,
  plus `clear_at_least`, `exclude_tools` and `clear_tool_inputs`); and memory as the `memory_20250818`
  tool, which the model calls and the application implements client-side.
- **Baseline failure modes.** Without context management the same run either hits a hard stop on a
  200K-token window, where the API rejects the next request, or keeps running on a 1M-token window while
  early material is buried under later tool results and recall degrades. The notebook adds that prefill
  latency scales with context length either way.
- **Trade-offs.** It summarizes the costs side by side: compaction trades verbatim detail for a
  summary and costs inference; clearing costs no inference but drops old results until they are
  re-fetched and invalidates cached prompt prefixes; memory adds tool-call overhead and is only as good
  as what the agent chose to save. Lossiness, it says, is a spectrum rather than a binary.
- **Composition.** Because each targets a different slice of the problem, the three compose rather
  than compete. When clearing is combined with the memory tool, it recommends excluding the memory
  tool from clearing so the agent does not lose track of what it just saved. It cites
  [[SoftwareApplication/claude-code]] as using compaction alongside two memory systems —
  [[DefinedTerm/claude-md]] files written by the developer and [[DefinedTerm/auto-memory]] written by
  Claude itself.
- **When to leave one out.** It suggests skipping memory when every session should start fresh,
  skipping compaction when sessions stay well under the context limit, and skipping clearing when the
  agent genuinely needs past tool results in full, for example for side-by-side comparison of passages.
- **Choosing by workload.** The closing guidance is to diagnose which part of the context problem a
  workload actually has before adding a primitive, and to treat its table of workload characteristics
  as hypotheses to test rather than answers. It also argues that a 1M-token window does not remove the
  need: context rot and prefill latency scale with how much is in the window, not with the window's
  limit.
- **Adjacent features.** It names [[DefinedTerm/programmatic-tool-calling]] and [[DefinedTerm/tool-search]] as
  different approaches to tool bloat that it does not cover.
