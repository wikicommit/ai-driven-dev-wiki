---
title: "Context Engineering: A Practical Guide for AI Agents (2026)"
type: "schema:BlogPosting"
lang: en
tags: [context-engineering, agentic-coding, agent-architecture, mcp]
sources:
  - type: url
    url: 'https://sourcegraph.com/blog/context-engineering'
    hash: sha256:004e8195be79c691c84abc9a3ab6d698b8815f7ee396e367c8aca94f56715dc3
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A Sourcegraph guide of 28 May 2026 by Matt Tanner organising [[DefinedTerm/context-engineering]] into four pillars — instructions, retrieval, memory, and tools — contrasting it with prompt engineering, and reporting the publisher's own retrieval benchmark results for coding agents."
  author:
    - "Matt Tanner"
  datePublished: "2026-05-28"
  publisher: "[[Organization/sourcegraph]]"
---

"Context Engineering: A Practical Guide for AI Agents (2026)" is a guide published on the [[Organization/sourcegraph]] blog on 28 May 2026 by Matt Tanner, a week after the same author's [[BlogPosting/agentic-coding-in-2026-a-practical-guide-for-big-code]]. Its stated audience is engineers "past the chatbot demo stage" who want agents to hold up in production.

Its framing premise is that by mid-2025 prompt wording had stopped being the main bottleneck, and the recurring problem became feeding an agent the right files, tool definitions, conversation slice, and retrieved facts at every turn "while keeping the context window from collapsing under its own weight." Its distinction between chatbots and agents makes the stakes concrete: an agent "tries to make a decision at step 47 with the residue of steps 1 through 46 still in its model's context window," and most context failures come from how a finite budget is spent rather than from a bad prompt at the front.

Like its companion, this is a vendor guide whose argument arrives at the publisher's own product; the four-pillar organisation and the failure-mode catalogue stand independently of that, while the benchmark numbers are the publisher's own measurements of its own tooling.

## Key Points

- **Four pillars.** The guide acknowledges that "different authors carve the space up slightly differently" — noting that the Prompting Guide lists hierarchical layers, Phil Schmid lists seven components, and Anthropic walks through system prompts, tools, examples, and message history without enumerating them — and offers four as a practical organisation. **Instructions**, the role, constraints, and output format the model holds before the first user message, where the stated failure is not length but "a mismatch with the model's training," since detailed instructions contradicting the model's default tool-use heuristics produce confused behaviour every turn. **Retrieval**, how external data enters the window, spanning RAG over a vector database, structured queries, file reads, and just-in-time retrieval using lightweight identifiers. **Memory**, split into short-term conversation history and long-term cross-session state, typically with a compaction step. **Tools**, described as where the discipline "gets the most ruthless," since each definition and each result costs tokens and ambiguous tool sets force the model to burn turns choosing between near-duplicates.
- **A layered rather than oppositional relation to prompt engineering.** The guide argues the two "sit at different layers of the stack" and offers a test for which you are doing: "If you're swapping nouns and adjectives, you're still doing prompt engineering. If you're changing what data the agent retrieves, in what order, with what re-ranking, and what gets evicted when the context window fills, you're doing context engineering." It reduces the discipline to four questions: what do we fetch, when do we fetch it, how do we compress it, and when do we throw it away.
- **Token budget management as pre-filtering.** Its definition is "the discipline of cutting low-signal content *before* it enters the context window, not after" — truncating tool outputs, compacting old conversation into a running summary, dropping retrieved chunks below a relevance threshold, and capping how many candidates each retrieval call contributes. It presents re-ranking as the step where naive RAG pipelines "either start working or stop working," illustrating with a pipeline that retrieves 50 candidates at high recall and re-ranks to a precise top-5 rather than dumping all 50 into the prompt.
- **A catalogue of failure modes.** Context overload, with the reported observation that agents performed worse with a 100K-token codebase summary than with a 5K-token targeted retrieval on the same task; **context distraction**, where irrelevant material crowds out important context; **context confusion**, where conflicting signals pull the model in different directions; **stale or irrelevant retrieval**, where unrefreshed embeddings leave an agent confidently calling a deprecated API it found in an old README; and **lost in the middle**, for which it quotes the Liu et al. paper's finding that performance "is often highest when relevant information occurs at the beginning or end of the input context, and significantly degrades when models must access relevant information in the middle of long contexts, even for explicitly long-context models." Its practical reading of the last is that assembly order matters — highest-signal material at the top or the bottom, not buried mid-way.
- **Structure beats similarity where structure exists.** For coding agents specifically, the guide argues that code has structure — call graphs, type information, cross-repository references — that text retrieval discards, so that a structural lookup turns "here are 50 files that mention the symbol" into "here is the one file where it's defined plus the three call sites." It is explicit that this is conditional: real-world coverage depends on indexing, language support, and permissions.
- **Bigger windows do not dissolve the problem.** Its stated position is that larger context windows reduce some pressure but not all of it, because latency and cost grow with size and the lost-in-the-middle and distraction patterns still apply: "Even at 2M tokens, you still want the LLM to see just what's useful for the current task."

- **The per-turn assembly pipeline.** The guide describes the order concretely: start from the user input and query, run one or more retrieval steps in parallel — vector search, keyword search, structured lookups, code-graph queries — and merge the results into a candidate set for the current task, then layer in memory, system instructions and tool definitions before the model call. In multi-agent systems, each subagent may run the same pipeline against a narrower scope before reporting back. This is what ties the four pillars into a single sequence rather than four separate concerns.
- **Why token budgets matter mechanically, not just for recall.** Beyond degradation in what a model attends to, the guide gives a cost argument: "in standard dense attention, cost scales quadratically with sequence length, and even with sparse-attention and flash-attention optimizations, larger context windows still increase latency, spend, and retrieval difficulty."
- **Instrumentation the guide prescribes.** Because "every additional retrieval, every additional tool call, every extra round of re-ranking shows up in p95 latency and per-task cost," it recommends tracking token usage and tool-call counts per task, setting budgets, and alerting when an agent class regularly exceeds them.

## Context

The guide credits Phil Schmid with helping popularize the term in mid-2025 and quotes his framing — designing dynamic systems that give a model the right information and tools, in the right format, at the right time. It also quotes [[Organization/anthropic]]'s definition of the discipline and its observation about tool sets: "If a human engineer can't definitively say which tool should be used in a given situation, an AI agent can't be expected to do better." Both appear here as the guide's citations of other parties rather than as its own formulations; the primary accounts are recorded on [[DefinedTerm/context-engineering]].

Its quantitative content is first-party. The publisher's own [[Dataset/codescalebench]] results, which the post dates to March 2026, are reported as running the same agent under two configurations across 370 enterprise-scale tasks, and the post also states that a February 2026 Sourcegraph 7.0 release positioned the company's code intelligence platform as "the shared intelligence layer for both developers and AI agents." Readers should treat the measured deltas as a vendor's evaluation of its own retrieval layer.
