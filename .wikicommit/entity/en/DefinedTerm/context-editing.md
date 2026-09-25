---
title: "Context editing"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, context-window, long-running-agents]
sources:
  - type: url
    url: 'https://www.anthropic.com/news/context-management'
    hash: sha256:2e78b9b42dd4fb917dd77e613ca45a3b65b4417a8499eb5d55167da969001cf6
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A context-management capability on the Claude Developer Platform that automatically clears stale tool calls and results from an agent's context window as it approaches token limits, while preserving the flow of the conversation."
---

Context editing is a capability that [[Organization/anthropic]] introduced on the Claude Developer Platform in September 2025, in [[BlogPosting/managing-context-on-the-claude-developer-platform]], which automatically clears stale tool calls and results from within an agent's context window when it approaches its token limits. Content that is no longer relevant is removed while the conversation flow is preserved, which Anthropic says extends how long an agent can run without manual intervention and raises effective model performance, since Claude then attends only to relevant context.

## Usage

Context editing addresses agents that accumulate tool results as they work and exhaust their effective context windows, a situation Anthropic describes as otherwise forcing developers to choose between cutting agent transcripts and degrading performance. It was announced together with the memory tool, a client-side, file-based store that persists across conversations (see [[DefinedTerm/structured-note-taking]]): context editing keeps the active window lean, while memory preserves what should outlast it. Anthropic's examples pair them — in coding, clearing old file reads and test results while memory keeps debugging insights and architectural decisions; in research, clearing old search results while memory keeps key findings.

Anthropic's own evaluation figures for the announcement are that, on an internal agentic-search evaluation set, context editing alone improved performance by 29% over baseline and 39% when combined with the memory tool, and that in a 100-turn web search evaluation it let agents finish workflows that would otherwise have failed from context exhaustion while reducing token consumption by 84%. At announcement it was in public beta on the Claude Developer Platform and through Amazon Bedrock and Google Cloud's Vertex AI.

The specific operation of replacing old tool results with a placeholder while keeping the record of each call is covered in more detail under [[DefinedTerm/tool-result-clearing]].

## Related Terms

- [[DefinedTerm/tool-result-clearing]]
- [[DefinedTerm/structured-note-taking]]
- [[DefinedTerm/compaction]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/context-rot]]
