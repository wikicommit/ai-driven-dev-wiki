---
title: "Effective context engineering for AI agents"
type: "schema:TechArticle"
lang: en
tags: [context-engineering, agent-architecture, agentic-coding]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
    hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A 29 September 2025 Anthropic engineering post setting out [[DefinedTerm/context-engineering]] as the successor to prompt engineering, arguing context is a finite attention budget and prescribing compaction, structured note-taking, and sub-agent architectures for long-horizon tasks."
  author: []
  datePublished: "2025-09-29"
  publisher: "[[Organization/anthropic]]"
  proficiencyLevel: "Expert"
---

"Effective context engineering for AI agents" is an engineering post published by [[Organization/anthropic]] on 29 September 2025, written by its Applied AI team. It argues that building with language models has shifted from finding the right words for a prompt to answering a broader question — "what configuration of context is most likely to generate our model's desired behavior?" — and offers a mental model plus a set of concrete techniques for the components of that configuration.

Its guiding principle, stated in one sentence and repeated in the conclusion, is that good context engineering means finding the smallest possible set of high-signal tokens that maximise the likelihood of a desired outcome. The post grounds this in a claim about model behaviour rather than about token limits: context should be treated as a finite resource with diminishing marginal returns, because models have an "attention budget" that every additional token depletes.

It is Anthropic's own account of practices it applies in its products, and several of its examples describe how Claude Code implements them; the recommendations are the company's, not a survey of the field.

## Key Practices

- **System prompts at the right altitude.** The post names two failure modes — hardcoding complex, brittle if-else logic to elicit exact behaviour, and giving vague high-level guidance that assumes shared context — and describes the optimal altitude as specific enough to guide behaviour yet flexible enough to leave the model strong heuristics. It recommends organising prompts into delineated sections, while noting exact formatting matters less as models improve, and starting from a minimal prompt on the best available model before adding instructions to address observed failures.
- **Tools that are token-efficient and unambiguous.** Tools should be self-contained, robust to error, and clear about their intended use. The post names bloated tool sets as one of the most common failure modes, with the test that if a human engineer cannot definitively say which tool applies in a situation, an agent will not do better.
- **Curated rather than exhaustive examples.** Few-shot prompting is strongly advised, but the post recommends against stuffing a laundry list of edge cases into a prompt, preferring a set of diverse, canonical examples that portray the expected behaviour.
- **Just-in-time context retrieval.** Rather than pre-processing all relevant data up front, agents maintain lightweight identifiers — file paths, stored queries, web links — and load data at runtime through tools. The post gives Claude Code writing targeted queries and using `head` and `tail` to analyse large data without loading it as its example, and argues the metadata of those references carries signal in itself: a file named `test_utils.py` in `tests/` implies something different from the same name in `src/core_logic/`. It notes the trade-off that runtime exploration is slower than retrieving pre-computed data, and describes a hybrid strategy — some data up front, further exploration at the agent's discretion — as what Claude Code actually does, with `CLAUDE.md` dropped into context up front while glob and grep retrieve files on demand.
- **Three techniques for long-horizon tasks.** [[DefinedTerm/compaction]], summarising a conversation nearing the context limit and reinitiating with the summary; structured note-taking, where an agent persists notes outside the context window and reads them back after a reset (see [[DefinedTerm/agentic-memory]]); and sub-agent architectures, where specialised sub-agents explore extensively in clean context windows and return condensed summaries of roughly 1,000–2,000 tokens (see [[DefinedTerm/multi-agent-orchestration]]). The post matches each to a task shape: compaction for work requiring extensive back-and-forth, note-taking for iterative development with clear milestones, and multi-agent for research and analysis where parallel exploration pays off.

## Scope & Caveats

The post's central empirical claim is [[DefinedTerm/context-rot]] — that as tokens in the context window increase, a model's ability to accurately recall information from that context decreases — which it attributes to research on needle-in-a-haystack benchmarking and explains through the transformer architecture's n² pairwise token relationships and through training distributions in which short sequences are more common. It characterises the result as a performance gradient rather than a hard cliff.

Two of its recommendations come with explicit hedges. On compaction, it warns that overly aggressive compaction loses subtle context whose importance only becomes apparent later, and advises tuning the compaction prompt on complex agent traces by first maximising recall and then improving precision. On the general direction of travel, it predicts that smarter models will require less prescriptive engineering and that "do the simplest thing that works" will remain the best advice — which means the specific techniques are offered as current practice rather than as durable architecture.
