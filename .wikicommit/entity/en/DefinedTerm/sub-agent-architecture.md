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
  - type: url
    url: 'https://www.anthropic.com/engineering/claude-code-best-practices'
    hash: sha256:9aae24f8b850a5f9c8a6f561be1fecf54f29e1ddc4658d00ecded22bccb82b82
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

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

Anthropic's Claude Code best-practices documentation describes two distinct jobs for the same
mechanism, and separating them is useful because they trade on different properties of a fresh
context. The first is **investigation**: because researching a codebase means reading many files and
every one of them consumes the main conversation's context, delegating the research to subagents that
explore separately and report back a summary keeps the main window clean for implementation. This is
the context-economy argument above, restated for a coding rather than a research setting.

The second is **adversarial review**, where the value is independence rather than economy. A reviewer
running in a fresh subagent context sees only the diff and the criteria it is given, not the reasoning
that produced the change, so it evaluates the result on its own terms — the documentation's framing is
that the longer an agent works unattended, the more an independent check matters before the work counts
as done. Because the reviewer runs as a subagent, its findings return directly to the implementing
session, which can fix them and re-review without a human ferrying findings between windows.

The same documentation states the failure mode of the second use plainly, and it is a caution worth
recording alongside the pattern: a reviewer prompted to find gaps will usually report some even when
the work is sound, because that is what it was asked to do. Chasing every finding is said to lead to
over-engineering — extra abstraction layers, defensive code, and tests for cases that cannot happen —
so the recommended mitigation is to instruct the reviewer to flag only gaps affecting correctness or
stated requirements, and to treat the rest as optional.

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
- [[DefinedTerm/code-review-agent]] — the review use above, treated as a subject in its own right
- [[DefinedTerm/llm-as-a-judge]] — the same independence argument applied to evaluation
- [[SoftwareApplication/claude-code]] — the tool whose documentation describes the two uses above
