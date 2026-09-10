---
title: "Prompt engineering"
type: "schema:DefinedTerm"
lang: en
tags: [llm, prompting]
sources:
  - type: url
    url: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
    hash: sha256:c7052e34d28ddebf93de128987f6d7d06951dc48afa9ec47e137b46b756c28b7
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "Methods for writing and organizing the instructions given to a language model for optimal outcomes, particularly system prompts."
---

Prompt engineering refers to methods for writing and organizing the instructions given to a
language model for optimal outcomes. As the term implies, its primary focus is how to write
effective prompts, and particularly system prompts. Anthropic describes it as having been the
biggest component of AI engineering work in the early days of building with LLMs, when the
majority of use cases outside everyday chat interactions required prompts optimised for one-shot
classification or text generation, and as having been the focus of attention in applied AI for a
few years before [[DefinedTerm/context-engineering]] came to prominence.

## Usage
Within a context-engineering frame, prompt writing becomes one component of
managing an entire context state that also includes tools, external data and message history, and
Anthropic's prompt-level guidance carries over into that larger practice: clear and direct
language at the right altitude, distinct sections marked with XML tagging or Markdown headers,
and the minimal set of information that still fully outlines the expected behaviour — where
minimal does not necessarily mean short.

## When It Applies
- Applies wherever the instructions given to a model are the main lever on its output. Anthropic
  identifies one-shot classification and text generation as the cases where this was the majority
  of the engineering work.
- Assumes the relevant state can be settled in advance, in writing. Anthropic argues this
  assumption breaks down for agents that operate over multiple turns of inference and longer time
  horizons, where information accumulates during the run and must be cyclically refined.
- Insufficient rather than wrong in the agentic setting: Anthropic presents context engineering
  as the natural progression of prompt engineering and as encompassing it, not as replacing it,
  and notes that the exact formatting of prompts is likely becoming less important as models
  become more capable.
- A well-established practice, described by Anthropic as the prior focus of applied AI work
  rather than as anything it proposes here.

## Related Terms
- [[DefinedTerm/context-engineering]]
