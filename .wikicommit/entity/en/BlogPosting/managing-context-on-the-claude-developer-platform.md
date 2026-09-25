---
title: "Managing context on the Claude Developer Platform"
type: "schema:BlogPosting"
lang: en
tags: [context-engineering, long-running-agents, memory]
sources:
  - type: url
    url: 'https://www.anthropic.com/news/context-management'
    hash: sha256:2e78b9b42dd4fb917dd77e613ca45a3b65b4417a8499eb5d55167da969001cf6
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Anthropic's September 2025 announcement of two context-management capabilities on the Claude Developer Platform — context editing, which clears stale tool calls and results as the context window fills, and the memory tool, a client-side file store that persists across conversations."
  datePublished: "2025-09-29"
  publisher: "[[Organization/anthropic]]"
---

The post introduces two capabilities on the Claude Developer Platform for managing an agent's context: [[DefinedTerm/context-editing]] and the memory tool. It starts from a production problem — agents that handle complex tasks and accumulate tool results tend to exhaust their effective context windows, leaving developers to choose between cutting agent transcripts and accepting degraded performance — and presents the two features as complementary answers: one keeps only relevant data in context, the other preserves valuable information across sessions.

[[Organization/anthropic]] released both alongside Claude Sonnet 4.5, which it says adds built-in context awareness by tracking available tokens through a conversation. They were announced in public beta on the Claude Developer Platform and through Amazon Bedrock and Google Cloud's Vertex AI.

## Key Points

- Context editing automatically clears stale tool calls and results from the context window when it approaches token limits, preserving the conversation flow; the post says this extends how long agents can run without manual intervention and improves effective model performance because Claude focuses only on relevant context.
- The memory tool lets Claude store and consult information outside the context window through a file-based system: Claude can create, read, update and delete files in a dedicated memory directory that persists across conversations (see [[DefinedTerm/structured-note-taking]]).
- The memory tool operates entirely client-side through tool calls, and the storage backend is in the developer's own infrastructure, so developers control where and how the data is persisted.
- The post's suggested division of labor by use case: in coding, context editing clears old file reads and test results while memory keeps debugging insights and architectural decisions; in research, memory stores key findings while old search results are cleared; in data processing, intermediate results go to memory while raw data is cleared.
- On an internal evaluation set for agentic search, Anthropic reports that combining the memory tool with context editing improved performance by 39% over baseline, and context editing alone by 29%.
- In a 100-turn web search evaluation, it reports that context editing let agents complete workflows that would otherwise have failed from context exhaustion, while cutting token consumption by 84%.

## Context

This is a vendor's product announcement, and its performance figures come from Anthropic's own internal evaluations. The two capabilities it introduces correspond to techniques this wiki covers in more depth elsewhere: clearing tool results from the transcript ([[DefinedTerm/tool-result-clearing]]) and agentic memory ([[DefinedTerm/structured-note-taking]]), both compared with [[DefinedTerm/compaction]] in [[TechArticle/context-engineering-memory-compaction-and-tool-clearing]].
