---
title: "Characterization Test"
type: "schema:DefinedTerm"
lang: en
tags: [tdd, ai-assisted-programming]
sources:
  - type: url
    url: 'https://agilejourney.uzabase.com/entry/2025/08/29/103000'
    hash: sha256:3ddb48b38b85526ba30bc0c2f6e032f2041384360d5a6e24c4261f8581fefe0d
    license: all-rights-reserved
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A test that records how existing code behaves now rather than how it ought to behave — an \"As-Is\" test rather than a \"To-Be\" one. It is the goal set nearer for legacy code whose intended behaviour has been lost, and a kind of test generative AI is reported to be extremely effective at producing."
---

A characterization test records how a piece of existing code actually behaves, rather than asserting how it ought to behave. Takuto Wada draws the contrast as "As-Is" against "To-Be": test-driven development needs To-Be tests, which verify what a program or system should do, but in legacy code that intention is frequently lost — there may be no specification, or one that has drifted badly from the code. Writing a To-Be test from nothing in that situation is too long a road, so the goal is set nearer: first capture how the code runs today.

## Usage

Wada reports that generative AI is extremely effective at this, and locates the reason in the shape of the request. Asking a model to capture the behaviour of existing code from a different angle and render it as an automated test is an after-the-fact task that can be given a narrowed context, unlike deciding how a system should behave — which he says a human has to reach by building skill, or by digging up past decisions as a piece of software archaeology.

Tsutomu Yasui identifies a second setting where the same test is what is wanted: the operations and maintenance phase after development has finished, when a team needs to capture current behaviour and be told if it breaks. He notes that maintenance teams are considerably smaller than development teams, and that people who are good at maintenance work are not necessarily practised at writing test code, which is what makes the AI assistance valuable there.

## When It Applies

It applies where there is no test coverage and no reliable account of intended behaviour. Wada's argument is that having As-Is tests alone lets a team detect defects and behaviour changes introduced by adding features, which is a large advance on having nothing — and that for an organization without the capacity for more, the value as a coverage-raising tool is already substantial.

Its limit is in what it captures. A characterization test records only how the code runs today; what the system ought to do is not in it, and on Wada's account that has to come from a human building the skill to decide it, or from digging up past decisions as software archaeology. He is explicit that To-Be tests remain the ideal and that this is a nearer goal rather than a substitute for them.

## Related Terms

[[DefinedTerm/red-green-tdd]], [[DefinedTerm/test-design]], [[DefinedTerm/test-list]]
