---
title: "Chat Templated Prompt"
type: "schema:DefinedTerm"
lang: en
tags: [llm-internals, coding-agents]
sources:
  - type: url
    url: 'https://simonwillison.net/guides/agentic-engineering-patterns/how-coding-agents-work/'
    hash: sha256:a8be3f0926e2b75d77e83036446bf575cf49b7dff42641018af0909da9d387eb
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A completion prompt laid out in a special format that represents an exchange with a model as a simulated conversation between labelled participants. Because models are stateless, the software around the model replays the whole conversation on every turn, which is why input token counts grow as a session lengthens."
---

A chat templated prompt is a completion prompt written in a special format that presents an
interaction with a language model as a simulated conversation, with each contribution labelled by
participant — `user:`, `assistant:`, and usually `system:`. Underneath it is still completion: the
natural continuation of a prompt ending in `assistant:` is for the model to answer the preceding
user turn. The format exists because the earliest models worked as bare completion engines, which
proved not to be user-friendly.

## Usage

The consequence that matters in practice follows from models being **stateless**: every execution
starts from the same blank slate. To maintain the illusion of a continuing conversation, the software
talking to the model keeps its own state and replays the entire existing exchange each time the user
adds a turn. Since providers charge for input as well as output tokens, this is why a conversation
becomes more expensive the longer it runs — the input grows on every turn. [[DefinedTerm/token-caching]]
is the pricing mechanism that partly offsets this, and the reason coding agents are built to avoid
modifying earlier conversation content.

The same format is what a tool call is expressed in. A system turn describes an available tool and
how to request it; the model ends its turn with a call; the harness extracts that request, executes
it, and appends the result as a further turn before asking the model to continue. On this account a
coding agent is not doing anything structurally exotic — it is assembling a chat templated prompt,
reading what comes back, and doing it again in a loop.

## Related Terms

[[DefinedTerm/token-caching]], [[DefinedTerm/ai-coding-agent]], [[DefinedTerm/prompt-engineering]],
[[DefinedTerm/context-engineering]], [[DefinedTerm/ai-agent]], [[DefinedTerm/compaction]]
