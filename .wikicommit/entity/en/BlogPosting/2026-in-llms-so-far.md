---
title: "2026 in LLMs (so far)"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, llm, ai-adoption, agent-safety, software-engineering]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Sep/27/2026-in-llms-so-far/'
    hash: sha256:385452beca91e7fc01c6dedad958d7ec1fa6f8605175db68befe2a8961aec188
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "Simon Willison's annotated slides and notes for his closing keynote at the WeAreDevelopers World Congress North America, a month-by-month tour of LLM developments from November 2025 to September 2026 with coding agents at its centre."
  author: ["Simon Willison"]
  datePublished: "2026-09-27"
---

This post is the annotated version of the closing keynote Simon Willison gave at the WeAreDevelopers
World Congress North America in San Jose in September 2026: each slide is reproduced with his notes,
arranged as a chronological tour of the year. He starts the year in November 2025, when the releases
of Claude Opus 4.5 and GPT-5.1 — incremental improvements in themselves — pushed their coding agents
across what he calls an invisible line, from "often make mistakes" to "reliable enough to use on a
day-to-day basis".

Most of what follows traces consequences of that shift for people who build software. He describes
the rise of [[SoftwareApplication/openclaw]] and the category of personal agents he calls
[[DefinedTerm/claw]]s, the [[DefinedTerm/software-factory]] rules [[Organization/strongdm]] described in
February, and two named feelings engineers have had about the change — [[DefinedTerm/deep-blue]] and
[[DefinedTerm/ai-mania]] — alongside [[DefinedTerm/tokenmaxxing]], a company-driven push for AI use
that rose and fell within months. He introduces the
idea of a [[DefinedTerm/fable-class-model]] and argues that what such models need from a user is close
to what software engineering already is. Running alongside are his informal "pelican riding a bicycle"
model comparisons, the rise of capable open-weight models that run on a laptop, and a series of
security incidents involving AI labs' agents in training, which he describes as still unfolding.

## Key Points

- Willison identifies November 2025 as an inflection point at which coding agents, paired with that
  month's new models, became reliable enough for day-to-day use.
- He calls OpenClaw "the most vibe-coded piece of software in existence" and says it effectively
  defined a new category of software, known by the generic term Claws, which he favours.
- He states that a Claw is really just a coding agent wearing a less threatening hat, working under the
  hood by writing and executing code on the user's computer.
- He reports StrongDM's two rules for software development — code must not be written by humans, and
  code must not be reviewed by humans — and says StrongDM were living six months ahead of everyone else
  in exploring how to be confident in software whose code no one reads.
- He says that many sessions at the conference were about code review and how far teams could get
  without it.
- He describes tokenmaxxing as rising and then falling within months, because agents turned out to be
  expensive, and says AI appears to have hit product-market fit in 2026 primarily through coding
  agents.
- He argues that a Fable class model can solve a clearly defined, unambiguously constrained problem by
  brute force given the right tools, and that defining goals, writing unambiguous instructions and
  choosing tools is "kind of what software engineering *is*".
- From his own experiments in prototyping games with coding agents, he concludes that it is easy to
  vibe-code something that looks like a game but that making one that is fun remained beyond him and
  beyond the agents he tried.
- He reports that his job feels harder rather than easier because the agent handles everything easy,
  and adopts Greg LeMond's line "It doesn't get easier, you just get faster" as a description of
  software engineering with coding agents.

## Context

The talk is one practitioner's account of a single year, written for a conference audience; the
predictions it revisits are ones Willison made himself on a podcast in January, and several of its
judgements — that LLMs now demonstrably write good code, or that a model's results show it to be in a
given class — are offered as his own reading rather than as measured findings. The pelican comparisons
are, in his own words, probably the world's stupidest benchmark, used because they still reveal
something about models within one family.

The concepts it introduces are covered on their own pages. On the question it keeps returning to —
how much of the engineer's job remains once agents write the code — its answer is that defining goals,
giving unambiguous instructions and choosing tools takes a lot of experience and skill, and that doing
it well gives an engineer "superpowers".
