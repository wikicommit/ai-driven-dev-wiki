---
title: "Compaction"
type: "schema:DefinedTerm"
lang: en
tags: [agents, context-window, long-horizon-tasks]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "The practice of summarising a conversation that is nearing the context window limit and reinitiating a new context window with that summary."
---

Compaction is the practice of taking a conversation nearing the context window limit, summarising
its contents, and reinitiating a new context window with the summary. Anthropic describes it as
typically the first lever in [[DefinedTerm/context-engineering]] for driving better long-term
coherence: at its core it distils the contents of a context window in a high-fidelity manner,
enabling an agent to continue with minimal performance degradation.

## Usage
In [[SoftwareApplication/claude-code]], Anthropic implements compaction by passing the message
history to the model to summarise and compress the most critical details. The model preserves
architectural decisions, unresolved bugs and implementation details while discarding redundant
tool outputs or messages; the agent then continues with that compressed context plus the five most
recently accessed files, so users get continuity without having to worry about context window
limitations.

Anthropic identifies clearing tool calls and results as low-hanging superfluous content — once a
tool has been called deep in the message history, the raw result generally need not be seen again
— and calls tool result clearing one of the safest, lightest-touch forms of compaction. It
describes this as having launched as a feature on the Claude Developer Platform.

## When It Applies
- Applies to long-horizon tasks where the token count exceeds the context window, and
  particularly to work requiring extensive back-and-forth; Anthropic says compaction maintains
  conversational flow for such tasks, in contrast to note-taking, which it says excels for
  iterative development with clear milestones.
- Assumes the message history can be summarised by a model, and that the compaction prompt has
  been tuned for the traces in question. Anthropic recommends carefully tuning that prompt on
  complex agent traces: first maximise recall so it captures every relevant piece of information
  from the trace, then iterate to improve precision by eliminating superfluous content.
- Fails when applied too aggressively. Anthropic says the art of compaction lies in selecting what
  to keep versus what to discard, and that overly aggressive compaction can lose subtle but
  critical context whose importance only becomes apparent later.
- Established as Anthropic's own implemented practice in Claude Code and as a shipped platform
  feature, described from its engineering experience rather than as a measured result.

## Related Terms
- [[DefinedTerm/structured-note-taking]]
- [[DefinedTerm/sub-agent-architecture]]
- [[DefinedTerm/context-engineering]]
