---
title: "AI Coding Agent"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/agentic-engineering/ai-coding-agent/'
    hash: sha256:bb64f869221b8e8a098760fd9b5e9036b0ac7f905aa9bbb025d181f3a42e4d9a
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "Software powered by a large language model that takes autonomous actions on a codebase: reading files, writing or editing code, executing commands, and iterating on the results."
---

An AI coding agent is software powered by a large language model that can take autonomous actions on a codebase. It reads files, understands the surrounding context, writes or edits code, executes commands, runs tests, and iterates based on the results it observes, rather than only suggesting what a person should type next.

## Usage

The defining property is autonomy: the agent operates in a loop, taking actions and observing results until a task is done, rather than predicting a single next line of code. It might create a file, notice a missing import, fix it, run the tests, see a failure, and adjust its approach without a person intervening at each step. Tools cited as examples of this category include Claude Code, Cursor, Windsurf, and GitHub Copilot's agent mode.

Coding agents are described as the foundation that agentic engineering is built on: without them, AI assistance is limited to autocomplete-style suggestions, whereas with them, whole tasks can be delegated and returned as working code. The quality of what an agent produces is described as depending heavily on the context it is given — clear specs, scaffolding, and guardrails — with agentic engineering named as the discipline of supplying that direction effectively.

In practice, this takes several shapes: a single-task agent that implements one described feature or fix end-to-end for a human to review; multi-agent setups where several agents work on different parts of a codebase at once; and background agents that run asynchronously on tasks like PR review or dependency updates while a person works on something else.

## Related Terms

The source names this term alongside [[DefinedTerm/tool-use]], [[DefinedTerm/plan-act-observe-loop]], [[DefinedTerm/guardrails]], [[DefinedTerm/human-in-the-loop]], and [[DefinedTerm/agentic-engineering]] as related glossary entries, without defining any of them.
