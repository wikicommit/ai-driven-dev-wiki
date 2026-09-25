---
title: "Context Engineering for Agents"
type: "schema:BlogPosting"
lang: en
tags: [context-engineering, agents, memory, multi-agent]
sources:
  - type: url
    url: 'https://rlancemartin.github.io/2025/06/23/context_engineering/'
    hash: sha256:872c48fe7b0d61366be4b7ec20669c465270485adca8e30165f5bd9cee4f66a2
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A June 2025 blog post by Lance Martin that groups the context-engineering strategies seen across popular agents into four buckets — write, select, compress and isolate — with examples of each."
  author: ["Lance Martin"]
  datePublished: "2025-06-23"
---

A post on Lance Martin's personal blog, published on June 23, 2025, that surveys how agents manage what
goes into their context window. It opens from the framing, which it attributes to Andrej Karpathy, of
the LLM as a new kind of operating system: the model is the CPU and its context window the RAM, a
working memory of limited capacity, and [[DefinedTerm/context-engineering]] is the job of filling that
window with just the right information for the next step. The post treats context engineering as an
umbrella over three kinds of context — instructions (prompts, memories, few-shot examples, tool
descriptions), knowledge (facts and memories), and tools (feedback from tool calls).

Its motivation is that agents, which interleave LLM calls with tool calls over long-running tasks,
accumulate tokens quickly, which can exceed the context window, raise cost and latency, or degrade
performance; it points to Drew Breunig's list of ways long contexts fail, including
[[DefinedTerm/context-poisoning]] and [[DefinedTerm/context-confusion]]. Against that, the post
proposes grouping the approaches in use into four buckets and illustrates each with examples from
products, papers and agent frameworks.

## Key Points

- **Write** — saving context outside the context window so that it is available to the agent. Within a
  session this is a scratchpad, implemented either as a tool call that writes to a file or as a field in
  the agent's runtime state; across sessions it is long-term memory, which the post traces from research
  such as Reflexion and Generative Agents into products including ChatGPT, Cursor and Windsurf.
- **Select** — pulling relevant context into the window. The post notes that many coding agents simply
  always load a narrow set of files, such as Claude Code's [[DefinedTerm/claude-md]] or Cursor's and
  Windsurf's rules files, while selecting from a large memory collection is harder and can go wrong, as
  when a memory is retrieved that the user did not expect. For tools, it describes applying retrieval to
  tool descriptions to fetch only the most relevant ones, and for knowledge it quotes a Windsurf engineer
  on why embedding search alone becomes unreliable as a codebase grows.
- **Compress** — keeping only the tokens a task needs, by summarization or by trimming. Its summarization
  example is Claude Code's auto-compact, which the post says runs after 95% of the context window is used
  and summarizes the full trajectory (see [[DefinedTerm/compaction]]); summarization can also be applied
  to token-heavy tool output or at agent-to-agent hand-offs. Trimming instead filters context with
  heuristics, such as removing older messages.
- **Isolate** — splitting context up, most commonly across sub-agents that each have their own tools,
  instructions and context window (see [[DefinedTerm/sub-agent-architecture]]). The post also describes
  isolating token-heavy objects in a code-execution sandbox, where an agent writes code whose results
  stay in the environment and only selected values return to the LLM, and in a runtime state object whose
  schema exposes only some fields to the model at each turn.
- The post relays Anthropic's report that multi-agent setups can use up to fifteen times more tokens than
  chat, alongside the need for careful prompting to plan sub-agent work and to coordinate sub-agents, as
  the costs of isolation — a figure it cites rather than measures.

## Context

The post presents its four buckets as a grouping of patterns already seen across popular agents, not as
a new technique, and says in closing that patterns for agent context engineering are still evolving. Most
of its supporting examples are cited from other organizations' writing — Anthropic, Cognition,
Hugging Face, OpenAI and LangGraph documentation among them — so the specifics it relays are those
sources' claims.
