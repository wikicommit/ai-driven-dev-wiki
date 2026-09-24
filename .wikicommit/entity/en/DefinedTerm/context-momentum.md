---
title: "Context Momentum"
type: "schema:DefinedTerm"
lang: en
tags: [vibe-coding, ai-assisted-programming]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2506.23253'
    hash: sha256:7d7ba02b9f8314bc08e972beb8a33d6aaaa26d4e697a4b41a334c3d682890e68
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A term from Sarkar and Drosos's study of vibe coding for the way the history of interactions and previously generated outputs in a session steer the subsequent direction of code generation, creating a form of path dependence."
---

Context momentum is the name Advait Sarkar and Ian Drosos give, in [[ScholarlyArticle/vibe-coding-programming-through-conversation-with-artificial-intelligence]], to the observation that within a [[DefinedTerm/vibe-coding]] session the history of interactions and the outputs already generated significantly influence the subsequent direction of code generation. It is the cumulative effect of the model's "interpretations" and the programmer's responses building on one another to shape the evolving intention for the program, and it creates a form of path dependence: early prompts and what they produce can set the project on a trajectory that becomes hard to diverge from later in the session.

## Usage

The authors compare it to the cognitive dimension of premature commitment, while noting that here it is hard to characterise as a property of a notation. Their example is an exchange-rate application whose developer asked for historical exchange-rate data; the model interpreted the request as a date picker for a single date, and the developer, finding that satisfactory, moved on. When the developer later explicitly asked for a date-range query in another part of the application, the newly generated code still fetched data for only a single date, which the developer attributed to the earlier implementation choice. The authors conclude that accepting edits that do not entirely match one's intent, to keep development fast, may make it harder later to communicate intent and steer the model.

They also note that context momentum can have positive, exploratory effects. In another session the developer's impromptu decision to add animations appeared to arise from possibilities presented by the structure of the existing generated code, so the goal itself depended on arbitrary but satisfactory implementation decisions the model had made.

The same paper reports that some vibe coders deliberately managed context — opening a new chat thread or closing all tabs before a new phase to "clear the context from the AI".

## Related Terms

- [[DefinedTerm/vibe-coding]]
- [[DefinedTerm/material-disengagement]]
