---
title: "Sub-agent architecture"
type: "schema:DefinedTerm"
lang: en
aliases: ["Multi-agent architecture"]
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
  description: "An arrangement in which specialised sub-agents handle focused tasks with clean context windows while a main agent coordinates from a high-level plan."
---

A sub-agent architecture is an arrangement in which specialised sub-agents handle focused tasks
with clean context windows, while a main agent coordinates the work from a high-level plan —
rather than one agent attempting to maintain state across an entire project. Anthropic presents it
as one of three techniques for working around context window limitations on long-horizon tasks,
alongside [[DefinedTerm/compaction]] and [[DefinedTerm/structured-note-taking]].

## Usage
The sub-agents perform the deep technical work, or use tools to find relevant information. Each
might explore extensively — Anthropic puts it at tens of thousands of tokens or more — but returns
only a condensed, distilled summary of its work, which it gives as often 1,000 to 2,000 tokens.
The result is a clear separation of concerns: the detailed search context remains isolated within
the sub-agents, while the lead agent focuses on synthesising and analysing the results.

## When It Applies
- Applies to complex research and analysis where parallel exploration pays dividends. Anthropic
  sets this against compaction, which it recommends for tasks requiring extensive back-and-forth,
  and note-taking, which it recommends for iterative development with clear milestones.
- Assumes a main agent holding a high-level plan and sub-agents that can be given focused tasks
  with fresh context windows, together with the convention that each returns a distilled summary
  rather than its full working context.
- Anthropic reports that the pattern showed a substantial improvement over single-agent systems on
  complex research tasks. The basis for that comparison is not stated alongside the claim, so the
  size of the improvement and the tasks it was measured on are not established here.

## Related Terms
- [[DefinedTerm/compaction]]
- [[DefinedTerm/structured-note-taking]]
- [[DefinedTerm/context-engineering]]
