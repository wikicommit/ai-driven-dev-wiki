---
title: "compaction"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, agent-architecture]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
    hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be
  - type: url
    url: 'https://www.langchain.com/blog/context-engineering-for-agents'
    hash: sha256:07e9475327ca11aeabb710cea3b419188e2ca4380d3cf4fd055291761f52fb8f
  - type: url
    url: 'https://code.claude.com/docs/en/best-practices'
    hash: sha256:92807ef3d58f63fbea435ea928df49e2f3341e118eb8c40db08800c100a4c4c5
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Taking a conversation approaching the context window limit, summarising its contents, and reinitiating a new context window with that summary — the usual first technique applied when an agent's session must outlast its context window."
  termCode: ""
  inDefinedTermSet: ""
---

Compaction is the practice of taking a conversation nearing the context window limit, summarising its contents, and reinitiating a new context window with the summary. [[TechArticle/effective-context-engineering-for-ai-agents]] gives that definition and describes it as typically the first lever reached for in [[DefinedTerm/context-engineering]] to drive better long-term coherence: at its core it distills a context window's contents in a high-fidelity manner so the agent can continue with minimal performance degradation.

## Usage

Anthropic describes its implementation in Claude Code as passing the message history to the model to summarise and compress the most critical details — preserving architectural decisions, unresolved bugs, and implementation details while discarding redundant tool outputs or messages — with the agent then continuing from that compressed context plus the five most recently accessed files. Its stated goal is that users get continuity without having to think about context window limits.

The Claude Code documentation exposes this to users as automatic compaction when approaching context limits, plus manual controls: `/compact <instructions>` to steer what is preserved, an example being `/compact Focus on the API changes`; a rewind menu offering "Summarize from here" and "Summarize up to here" to condense only part of a conversation; and instructions in `CLAUDE.md` to customise the behaviour, its example being "When compacting, always preserve the full list of modified files and any test commands." It also recommends `/clear` between unrelated tasks as the blunter alternative — resetting context entirely rather than summarising it.

[[BlogPosting/context-engineering]] places compaction in its "compress" bucket, distinguishing summarization, which uses a model to distill, from **trimming**, which filters or prunes by hard-coded heuristics such as removing older messages. It notes summarization can be applied at points other than the end of a conversation — after token-heavy tool calls, or at agent-to-agent boundaries to reduce tokens during knowledge hand-off — and relays that Cognition uses a fine-tuned model for the step, which it presents as an indication of how much work can go into it.

The named risk is loss. Anthropic warns that overly aggressive compaction can discard subtle but critical context whose importance only becomes apparent later, and recommends tuning the compaction prompt on complex agent traces by first maximising recall and then improving precision. Its example of safe, low-hanging compaction is tool result clearing: once a tool has been called deep in the message history, the agent rarely needs to see the raw result again.

## Related Terms

Compaction is one of three standard techniques for long-horizon work, alongside [[DefinedTerm/agentic-memory]] and [[DefinedTerm/multi-agent-orchestration]]; Anthropic matches it specifically to tasks requiring extensive back-and-forth. [[DefinedTerm/adaptive-context-compaction]] describes a more specific variant in which reduction is applied in graduated stages as context pressure rises rather than as a single event at a hard limit. The underlying problem it exists to manage is [[DefinedTerm/context-rot]].
