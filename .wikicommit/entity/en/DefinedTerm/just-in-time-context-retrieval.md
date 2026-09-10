---
title: "Just-in-time context retrieval"
type: "schema:DefinedTerm"
lang: en
aliases: ["Just in time context"]
tags: [agents, context-window, retrieval]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "An approach in which an agent holds only lightweight identifiers and uses tools to load the underlying data into context at runtime, rather than pre-processing all relevant data up front."
---

Just-in-time context retrieval is an approach in which an agent maintains only lightweight
identifiers — file paths, stored queries, web links and the like — and uses those references to
load data into its context dynamically at runtime through tools, rather than pre-processing all
potentially relevant data up front. Anthropic describes it as the direction engineers are moving
as applications become more agentic, with teams augmenting the embedding-based, pre-inference-time
retrieval systems common in AI-native applications with these runtime strategies.

## Usage
Anthropic compares the approach to human cognition: people generally do not memorise entire
corpuses of information but introduce external organisation and indexing systems — file systems,
inboxes, bookmarks — to retrieve what is relevant on demand. Beyond storage efficiency, the
metadata of the references themselves carries signal. To an agent operating in a file system, a
file named `test_utils.py` in a `tests` folder implies a different purpose from a file of the same
name under `src/core_logic/`, and folder hierarchies, naming conventions and timestamps all
indicate how and when information should be used.

Letting agents navigate and retrieve data autonomously also enables progressive disclosure —
incrementally discovering relevant context through exploration, where file sizes suggest
complexity, naming conventions hint at purpose, and timestamps act as a proxy for relevance. Each
interaction yields context that informs the next decision, so the agent assembles understanding
layer by layer, keeping only what is necessary in working memory and using note-taking strategies
for anything that must persist further.

## When It Applies
- Applies where the data is large or changing and the agent can be given tools to reach it.
  Anthropic's own agentic coding tool [[SoftwareApplication/claude-code]] uses the approach to
  perform complex data analysis over large databases: the model writes targeted queries, stores
  results, and leverages Bash commands such as `head` and `tail` to analyse large volumes of data
  without ever loading the full data objects into context.
- Assumes opinionated and thoughtful engineering of the tools and heuristics an agent uses to
  navigate its information landscape. Anthropic is explicit that without proper guidance an agent
  can waste context by misusing tools, chasing dead ends, or failing to identify key information.
- Its cost is speed: runtime exploration is slower than retrieving pre-computed data. Anthropic
  suggests that the most effective agents may employ a hybrid strategy — retrieving some data up
  front for speed and pursuing further autonomous exploration at their discretion — and that the
  hybrid may be better suited to contexts with less dynamic content, such as legal or finance
  work. Claude Code is given as an example, with CLAUDE.md files dropped into context up front
  while primitives such as glob and grep retrieve files just in time, bypassing the issues of
  stale indexing and complex syntax trees.
- Presented as Anthropic's reading of where the field is converging, drawn from its own product
  experience and from working with customers rather than from a measured comparison. Anthropic
  expects agentic design to trend toward progressively less human curation as model capabilities
  improve.

## Related Terms
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/structured-note-taking]]
