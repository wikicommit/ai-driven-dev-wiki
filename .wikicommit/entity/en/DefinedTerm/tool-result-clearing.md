---
title: "Tool-result clearing"
type: "schema:DefinedTerm"
lang: en
aliases: ["Tool clearing"]
tags: [context-engineering, context-window, long-horizon-tasks, tool-use]
sources:
  - type: url
    url: 'https://platform.claude.com/cookbook/tool-use-context-engineering-context-engineering-tools'
    hash: sha256:ff18c6ce4f289fc1d0603542473d89de2170efe173360a83c70d460ec9204888
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A context-engineering technique that replaces old, re-fetchable tool results in an agent's conversation with a short placeholder while keeping the record that each tool call was made, bounding context growth without any inference cost."
---

Tool-result clearing is a context-engineering technique for long-running agents in which old tool
results in the conversation history are replaced with a short placeholder, while the preceding tool-call
record — which tool was called, and with what input — is left in place. It targets the bloat that tool
use itself produces: every tool result is carried forward and counts against the input-token budget on
every later turn, even after the agent has processed it and moved on, yet much of that content (file
contents, API responses, search results) can simply be fetched again if it is needed. Anthropic's
[[TechArticle/context-engineering-memory-compaction-and-tool-clearing]] describes it as a
*sub-transcript* operation, in contrast to [[DefinedTerm/compaction]], which summarizes the whole
transcript: user messages, the agent's reasoning and the tool-call records are untouched, and only the
bulky payloads are dropped.

## Usage

The notebook shows the mechanism as walking the message list and replacing the content of all but the
most recent few tool results with a placeholder. Anthropic's API provides it as the
`clear_tool_uses_20250919` context edit, which handles token counting and triggering server-side,
preserves the pairing between tool calls and their results, and lets specific tools be exempted from
clearing. Its knobs are numeric or list-based rather than a prompt: a token `trigger` (default 100K),
how many recent tool uses to `keep` (default three), a minimum amount to `clear_at_least`, the tools to
exclude, and whether to clear tool inputs as well. When clearing fires, the response reports how many
tool uses were cleared and how many tokens were freed, which the notebook recommends using to compare
configurations against one's own workload.

The notebook calls clearing the cheapest of the three primitives it compares — no inference, just a
mechanical edit to the message list — and describes it as lossless as long as the tool can be called
again. When clearing is combined with the memory tool (see [[DefinedTerm/structured-note-taking]]), it
recommends excluding the memory tool from clearing so that the agent does not lose track of what it has
just saved.

## When It Applies

- **Conditions.** It suits workloads whose context is dominated by large, re-fetchable tool results
  such as file reads and API responses. It does nothing for context that is not a tool result — the
  agent's own reasoning or user messages — and provides no persistence across sessions.
- **Assumptions.** It assumes the cleared results can be re-fetched when needed, and cheaply. The
  notebook notes that re-reading a local file is nearly free while re-calling a rate-limited or slow API
  is not, and suggests preferring compaction over clearing for tool results that are not easily
  re-fetched, such as ephemeral APIs or uploads.
- **Failure modes.** After clearing, the agent must either work from its own notes and whatever recent
  results survived, missing details it saw but did not record, or re-read cleared content, which can
  mean more tool calls than without clearing. Clearing also invalidates cached prompt prefixes; the
  `clear_at_least` setting exists so that each clearing frees enough tokens to make that worthwhile. The
  notebook advises skipping clearing when the agent genuinely needs past tool results in full, as in
  side-by-side comparison of passages across documents.
- **How established.** It is presented as Anthropic's own guidance and a shipped API feature,
  demonstrated on a synthetic research-agent workload; the notebook treats the right `trigger` and
  `keep` values as workload-specific and to be found by testing.

## Related Terms

- [[DefinedTerm/compaction]]
- [[DefinedTerm/structured-note-taking]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/context-rot]]
- [[DefinedTerm/observation-masking]]
