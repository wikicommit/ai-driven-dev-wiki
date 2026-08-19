---
title: "Adaptive Context Compaction"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, agent-architecture, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.05344'
    hash: sha256:29a5dfd46c7505affc599f6922ebba2f67d01e7f3a343df5347a42f435a08edc
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A framework for managing an agent's context window through a pipeline of progressively aggressive reduction stages triggered at rising pressure thresholds, rather than a single lossy summarization performed once a hard limit is reached."
  termCode: "ACC"
---

Adaptive Context Compaction (ACC) is a context-management framework described in [[ScholarlyArticle/building-effective-ai-coding-agents-for-the-terminal]] that manages context pressure through a pipeline of progressively aggressive reduction strategies, monitored at the start of every reasoning iteration. It is presented as an alternative to what the report characterizes as the standard approach: a binary emergency threshold, typically triggered at 95–99% capacity, that performs a lossy summarization of the conversation history — resulting in late activation, severe information loss, and compounding errors on subsequent compactions.

## Usage

The motivating observation is that tool observations such as file contents and command outputs accumulate quickly and frequently consume 70–80% of the available token budget. ACC therefore monitors token usage incrementally, using the API's reported prompt token count as a calibration anchor, and applies five graduated stages:

| Stage | Trigger | Action |
| --- | --- | --- |
| Warning | 70% | Context pressure is logged for monitoring; no data reduction occurs |
| Observation masking | 80% | Older tool result messages are replaced in place with compact reference pointers; the most recent outputs are preserved at full fidelity |
| Fast pruning | 85% | A lightweight pass walks backward through tool results and replaces those beyond a protected recency budget with pruned markers |
| Aggressive masking | 90% | The preservation window shrinks to only the most recent tool outputs; all other observations are masked |
| Full compaction | 99% | The entire conversation history is serialized to a scratch file and an LLM-based summarizer compresses the middle portion while preserving recent messages verbatim |

The report distinguishes masking from pruning: masking replaces content with reference pointers to offloaded files, while pruning is a deletion-class operation that discards content, but targets only outputs well beyond the recency window. It notes that the cheaper strategies often reclaim enough space to avoid the more disruptive stages entirely — the fast pruning pass in particular is described as substantially cheaper than LLM-based compaction.

Two mechanisms are described as making compaction effectively non-lossy. The pipeline maintains an *artifact index*, a structured registry of all files touched and operations performed during the session, which is serialized into the compaction summary so the agent remembers what files it has worked with even after context is compressed. The history archive path is also injected into the summary, so the agent can recover any detail by reading the archive.

The report states that quantitative evaluations show ACC reduces peak context consumption of observations by approximately 54%, often eliminating the need for emergency compaction entirely over typical 30-turn sessions.

Its author generalizes the design into a lesson: context reduction is not a binary operation, and a graduated approach — monitoring utilization continuously, pruning stale tool outputs before they become irrelevant, masking old observations, and reserving LLM-based summarization for genuine overflow — dramatically outperforms compacting everything once a hard limit is reached. He also notes that the specific threshold values resist first-principles calculation and emerged from iterative failure analysis rather than analytical derivation.

## Related Terms

ACC is one of the mechanisms grouped under [[DefinedTerm/context-engineering]], and one of the concerns the [[DefinedTerm/agent-harness]] coordinates at runtime. The report describes it as complementary to tool result summarization at ingestion: because results are already compressed when they enter the conversation, the input to the summarizing model during full compaction is itself substantially smaller.
