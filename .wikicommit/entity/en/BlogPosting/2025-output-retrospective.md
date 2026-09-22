---
title: "2025年のアウトプットふりかえり"
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, coding-agents, tdd, ai-assisted-programming, terminology]
sources:
  - type: url
    url: 'https://t-wada.hatenablog.jp/entry/2025-retrospective'
    hash: sha256:2ad331276c8ab3f6b03b8b53b2981d1cc1f36083a08fbd7a1e61e228b92c5e23
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A Japanese testing and TDD practitioner's month-by-month record of his 2025, doubling as a first-hand timeline of the year coding agents arrived: when he adopted one, what changed when it became flat-rate, how his training material had to be rebuilt, and his claim that agents were what finally made automated testing ordinary."
  author: ["Takuto Wada"]
  datePublished: "2026-01-06"
---

The post is a month-by-month record of one practitioner's 2025 output, written because the author had
occasion to compile it for work. What makes it more than a list is its opening premise — that 2025
will be remembered as the year the way software is made changed substantially — and the fact that the
author's subject for the preceding two decades has been automated testing and test-driven
development, so the year's changes landed directly on his material. He also states plainly that the
post is entirely his own writing, with AI involved in neither its prose nor its structure.

Read as a timeline, it is unusually specific about when things turned. He describes his own mood at
the end of 2024 as gloomy, watching coding agents grow capable and the territory where humans write
code start to be cut away, and wondering whether people would write code at all. February is where he
puts the decisive month, naming three publications from it — two on consecutive days and a third
later that month — and summarising their combined effect as the human moving from the driver's seat
to the passenger seat and the AI moving the other way. In March, on hearing that a coding agent usable from the CLI had appeared, he starts using
[[SoftwareApplication/claude-code]] straight away; with his editor no longer pinned by the agent he
returned to Emacs, and switched terminal too. In May the pricing
change lands, and he identifies it immediately as decisive: with a flat monthly rate rather than
per-token billing, he could iterate without watching the meter, and what he could see changed.

The professional consequences run alongside. New-hire training had to be restructured, because he had
to decide how to teach [[DefinedTerm/red-green-tdd]] in an era when agents write the code; his
solution was a two-part format teaching the current situation and then the enduring design
fundamentals behind it. He notes that in demonstrations, new engineers responded more strongly to
watching a specification be argued out with a model than to watching code be written test-first. The
year's most-read deck of his was a completely new talk on software development in the age of AI,
written and rewritten in a green room the morning it was delivered. In December he ran a
[[DefinedTerm/spec-driven-development]] training course for the first time, and reports the
difficulty that makes such courses hard to guarantee: an agent's behaviour is probabilistic, so the
quality of the experience is hard to assure.

## Key Points

- The post's framing claim is that 2025 will be remembered as the year the way software is made
  changed substantially, and the author states it was a particularly memorable year for him
  personally.
- The author states explicitly that the entry is 100% his own writing and that AI was involved in
  neither its content nor its structure.
- His recorded state of mind at the end of 2024 was unsettled: coding agents were growing rapidly
  capable, the area in which humans write code was beginning to be pared away, and he records
  wondering whether humans would write code at all, while noting he loves coding.
- He dates the decisive shift to February 2025, naming three publications from that month —
  including one he credits with making [[DefinedTerm/vibe-coding]] a talking point — and summarises
  their combined effect as the human moving from the driver's seat to the passenger seat while the AI
  moved from passenger to driver.
- He began using Claude Code in March 2025, reporting that he started as soon as he heard a coding
  agent usable from the CLI had appeared; the consequence he records is that his editor was no longer
  constrained to VS Code, so he moved back to Emacs and kept that configuration for the rest of the
  year.
- He identifies the May 2025 change that made Claude Code available under a flat-rate subscription
  as decisive, on the stated grounds that it changed the incentive structure: without per-request
  billing to watch, he could experiment aggressively, and what he could see changed as a result.
- Before Claude Code gained a planning mode, his workflow was to settle the specification in a chat
  interface first and only then move to the agent — and he reports new engineers in his training
  reacting more strongly to that specification discussion than to writing code test-first.
- Restructuring his standing new-hire training was a genuine difficulty for him: he records not
  knowing how TDD should be taught, or what career to describe, in an era when coding agents write
  the code, and settled on a two-part format covering the present situation and then the underlying
  design fundamentals.
- He reports a client explicitly commissioning half-formed material — asking him to speak on TDD in
  the age of AI even if it was not fully worked out — and treats that as a challenging but welcome
  kind of request.
- A practitioner's finding is recorded from June: that instructing Claude Code to follow this
  author's own recommended approach is markedly effective at getting it to do TDD. The author's
  reading of why is that the terms TDD and test-driven development spread so widely that their
  meaning thinned, becoming confused with automated testing and test-first, which affected LLM
  training data — and that supplying a person's name gives the model a concrete reference point that
  narrows it to a specific style (see [[BlogPosting/making-ai-do-t-wada-style-tdd]]).
- His own open-source work that month went the other way: he developed a new output format for his
  assertion library aimed at being LLM-friendly, and states that no AI wrote that code — he wrote
  100% of it himself. His stated motivation is that an era in which agents run tests frequently and
  judge the results needs both ease of writing tests and informative failure output.
- He ran his first spec-driven development training course in December 2025, and reports the problem
  it exposed: because an agent's behaviour is probabilistic, assuring the quality of a training
  experience built on one is difficult, and he expects to keep searching for a workable format.
- His summed 2025 output is 53 talks, 12 training courses, 10 panel discussions, 6 podcast
  recordings, 5 question-and-answer events, 4 interviews and one book published as supervising
  translator, with his talk on software development in the age of AI given 15 times.
- Two of his 2025 decks were nominated in the year's most-viewed presentations on the platform he
  publishes them to: the one on software development in the age of AI and one on judging technology
  choices.
- His closing claim is the one with the widest reach: that after nearly twenty years of advocating
  automated testing, test-first and TDD in Japan, 2025 was the year automated testing became most
  widespread, because AI agents substantially reduced the two obstacles in its way — learning cost
  and implementation cost — and that automated testing has finally become ordinary.
- He immediately qualifies it: the accompanying [[DefinedTerm/semantic-diffusion]] is severe, and his
  stated remedy is simply to keep explaining, patiently, again.
- The post closes on a reversal of its own opening: the gloom of January 2025 had lifted, replaced by
  a readiness to play under the new rules of the game.

## Context

This is a personal retrospective rather than an argument, and its evidential status varies by claim:
the counts of talks and courses are the author's own records, while the assessments — which month was
decisive, what the pricing change meant, whether automated testing has become ordinary — are his
judgment from one vantage, that of a Japanese testing specialist whose consulting and training work
put him in front of many organisations during the year. That vantage is the post's main value and
also its limit: the claim that automated testing became widespread in 2025 is offered as what he
feels rather than as measurement, and he says so. Several of the publications and events he credits
with turning the year are linked rather than described, and their own contents are not established
here. The term-thinning he names at the end is treated as its own subject under
[[DefinedTerm/semantic-diffusion]], and the practice whose adoption he tracks under
[[DefinedTerm/agentic-coding]].
