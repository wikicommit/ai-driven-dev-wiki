---
title: "Context Engineering"
type: "schema:BlogPosting"
lang: en
tags: [context-engineering, agents, memory, multi-agent]
sources:
  - type: url
    url: 'https://blog.langchain.com/context-engineering-for-agents/'
    hash: sha256:8117f9ce8bfc2d31c554ae40e47e44aea14ddecd56eea8f73a6cb9c2ce29ffff
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A July 2025 LangChain blog post that groups the context-engineering strategies seen across popular agents into four buckets — write, select, compress and isolate — and maps each to LangGraph features, with LangSmith offered for tracing and evaluation."
  author: ["The LangChain Team"]
  datePublished: "2025-07-02"
  publisher: "LangChain"
---

A post on LangChain's blog, credited to the LangChain Team and dated July 2, 2025, about how agents manage
what goes into their context window. It opens with the framing, which it attributes to Andrej Karpathy,
of the LLM as a new kind of operating system in which the model is the CPU and its context window the RAM,
and quotes his description of [[DefinedTerm/context-engineering]] as the delicate art and science of
filling the context window with just the right information for the next step. It treats context
engineering as an umbrella over three kinds of context: instructions (prompts, memories, few-shot
examples, tool descriptions), knowledge (facts and memories), and tools (feedback from tool calls).

Its motivation is that agents, which interleave LLM calls and tool calls over long-running tasks,
accumulate tokens that can exceed the context window, raise cost and latency, or degrade performance; it
points to Drew Breunig's list of ways long contexts fail, including [[DefinedTerm/context-poisoning]] and
[[DefinedTerm/context-confusion]]. It then groups the strategies in use into four buckets, with examples
drawn from agent products and papers, and closes by mapping each bucket to features of LangChain's own
[[SoftwareApplication/langgraph]], with LangSmith offered for tracing token usage and testing the impact
of context-engineering changes.

## Key Points

- **Write** — saving context outside the context window: a scratchpad within a session, implemented as a
  tool call that writes to a file or as a field in the agent's runtime state object, and long-term
  memories across sessions, which the post traces from research such as Reflexion and Generative Agents
  into products including ChatGPT, Cursor and Windsurf.
- **Select** — pulling relevant context into the window. Many coding agents always load a narrow set of
  files, such as Claude Code's [[DefinedTerm/claude-md]] or Cursor's and Windsurf's rules files, while
  selecting from a large memory collection is harder and can surprise users; for tools, the post
  describes retrieving only the most relevant tool descriptions, and for knowledge it quotes "Varun from
  Windsurf" on why embedding search alone becomes unreliable as a codebase grows.
- **Compress** — keeping only the tokens a task needs, by summarization, such as Claude Code's
  auto-compact, which the post says runs after 95% of the context window is used (see
  [[DefinedTerm/compaction]]), or post-processing of token-heavy tool output and agent-to-agent
  hand-offs; or by trimming with heuristics such as dropping older messages.
- **Isolate** — splitting context up, most commonly across sub-agents with their own tools, instructions
  and context windows (see [[DefinedTerm/sub-agent-architecture]]), and also by keeping token-heavy
  objects in a code-execution sandbox or in fields of a state object that are not exposed to the model at
  every turn.
- As the costs of multi-agent isolation, the post relays Anthropic's report of up to fifteen times more
  tokens than chat, alongside the need for careful prompting to plan sub-agent work and for coordination —
  a figure it cites rather than measures.
- Before applying any of these, the post recommends two foundations: a way to look at your data and track
  token usage across the agent, and a simple way to test whether a context-engineering change helps or
  hurts; it offers LangSmith tracing and evaluation for both.
- For each bucket it maps a LangGraph feature: checkpointed thread-scoped state as a scratchpad and
  long-term memory across sessions for writing; per-node access to state and memory retrieval for
  selecting, with the LangGraph Bigtool library for semantic search over tool descriptions; summarization
  or trimming utilities and custom summarization nodes for compressing; and a state schema, sandboxes and
  supervisor and swarm libraries for isolating.

## Context

The post presents its four buckets as a grouping of patterns already seen across popular agents rather
than as a new technique, and much of its supporting evidence is quoted from other organisations' writing —
Anthropic, Cognition and Hugging Face among them — so those specifics are those sources' claims. Its
closing section is LangChain's description of its own products, and its recommendations for LangGraph and
LangSmith should be read as vendor guidance.
