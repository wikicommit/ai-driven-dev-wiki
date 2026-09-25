---
title: "Tool Call Offloading"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, harness-engineering, context-window]
sources:
  - type: url
    url: 'https://blog.langchain.com/the-anatomy-of-an-agent-harness/'
    hash: sha256:71cffd4adc7b81b7dd5f981d26af2bebcee592b2751a882ea95bb833fa2d022e
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A harness technique that keeps only the head and tail of a large tool output in an agent's context and writes the full output to the filesystem, where the model can read it if it needs to."
---

Tool call offloading is a harness technique for limiting the effect of large tool outputs on an agent's
context window. When a tool's output exceeds a threshold number of tokens, the harness keeps only the
head and tail tokens of that output in context and offloads the full output to the filesystem, so that
the model can still access it if needed. LangChain's
[[BlogPosting/the-anatomy-of-an-agent-harness]] describes it as a way to reduce the impact of outputs
that clutter the context window noisily without providing useful information.

## Usage

The term is used in [[DefinedTerm/harness-engineering]] as one of the strategies a harness applies
against [[DefinedTerm/context-rot]], the degradation of a model's reasoning and task completion as its
context fills. The same post groups it with [[DefinedTerm/compaction]], which summarizes and offloads the
existing context when the window is nearly full, and with Skills, which use
[[DefinedTerm/progressive-disclosure]] to avoid loading every tool at start. It depends on a filesystem
the agent can read, which that post treats as the most foundational harness primitive.

## Related Terms

- [[DefinedTerm/context-rot]]
- [[DefinedTerm/compaction]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/progressive-disclosure]]
