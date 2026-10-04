---
title: "Fable Class Model"
type: "schema:DefinedTerm"
lang: en
tags: [llm, coding-agents, software-engineering]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Sep/27/2026-in-llms-so-far/'
    hash: sha256:385452beca91e7fc01c6dedad958d7ec1fa6f8605175db68befe2a8961aec188
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "Simon Willison's name for a class of model, first glimpsed publicly with Claude Fable 5, that will solve a problem effectively by brute force if given a clearly defined goal, unambiguous instructions about its constraints, and access to the necessary tools."
---

A Fable class model, as Simon Willison uses the phrase in [[BlogPosting/2026-in-llms-so-far]], is a
model that will solve your problem effectively through brute force provided three things are in place:
the goal for what you want to build is **clearly defined**, the constraints around that goal are given
as **unambiguous instructions**, and the model has **access to the necessary tools** to achieve it. He
names the class after Claude Fable 5, released in June 2026, which he calls the first public glimpse
of such a model, and counts GPT-6 Astra and GPT-5.6 among others he places in it.

## Usage

Willison draws two readings from the idea. On one hand it looks like a direct threat to software
engineers, because it means models can build effectively any piece of software that can be defined in
this way. On the other, he argues, defining goals, providing unambiguous instructions and working out
the right tools are "kind of what software engineering *is*": doing them well takes a lot of
experience and skill, and someone who can do them well now has, in his word, superpowers. He says this
realisation — that there is still a lot of skill in driving models this capable — helped him somewhat
with the feeling he calls [[DefinedTerm/deep-blue]].

The category is his own informal one. His placement of particular models in it rests on his own use
and comparisons, such as calling GPT-5.6 "definitely a Fable class model" while judging it possibly not
quite as good as Fable.

## Related Terms

[[DefinedTerm/deep-blue]], [[DefinedTerm/spec-driven-development]], [[DefinedTerm/ai-coding-agent]]
