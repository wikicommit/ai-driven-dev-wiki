---
title: "Characterization Test"
type: "schema:DefinedTerm"
lang: en
tags: [tdd, ai-assisted-programming, legacy-code]
sources:
  - type: url
    url: 'https://agilejourney.uzabase.com/entry/2025/08/29/103000'
    hash: sha256:3ddb48b38b85526ba30bc0c2f6e032f2041384360d5a6e24c4261f8581fefe0d
    license: all-rights-reserved
  - type: url
    url: 'https://addyosmani.com/blog/brownfield-agentic-engineering/'
    hash: sha256:9e908973327fcd790eb88436c8412c9fc0a9343a93e8ec27945dd2416438a811
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A test that records how existing code behaves now rather than how it ought to behave — an \"As-Is\" test rather than a \"To-Be\" one. It is the goal set nearer for legacy code whose intended behaviour has been lost, and a kind of test generative AI is reported to be extremely effective at producing."
---

A characterization test records how a piece of existing code actually behaves, rather than asserting how it ought to behave. Takuto Wada draws the contrast as "As-Is" against "To-Be": test-driven development needs To-Be tests, which verify what a program or system should do, but in legacy code that intention is frequently lost — there may be no specification, or one that has drifted badly from the code. Writing a To-Be test from nothing in that situation is too long a road, so the goal is set nearer: first capture how the code runs today.

## Usage

Wada reports that generative AI is extremely effective at this, and locates the reason in the shape of the request. Asking a model to capture the behaviour of existing code from a different angle and render it as an automated test is an after-the-fact task that can be given a narrowed context, unlike deciding how a system should behave — which he says a human has to reach by building skill, or by digging up past decisions as a piece of software archaeology.

Tsutomu Yasui identifies a second setting where the same test is what is wanted: the operations and maintenance phase after development has finished, when a team needs to capture current behaviour and be told if it breaks. He notes that maintenance teams are considerably smaller than development teams, and that people who are good at maintenance work are not necessarily practised at writing test code, which is what makes the AI assistance valuable there.

Addy Osmani places the same test at the start of bringing coding agents into a brownfield codebase, in
[[BlogPosting/brownfield-agentic-engineering]]. He defines characterization tests as automated tests
"used to document a system's actual current behavior so you can safely refactor or change legacy
code," and stresses that they pin down what a module does today "ugly parts included," because in an
old system some of that ugly behaviour is what the business runs on and an agent will happily "fix"
it behind a green suite. In his zoning of a codebase by risk, they are the gate for the middle tier:
agents may change code of mixed quality only after characterization tests have been written, and
such a zone is promoted to the low-risk tier once the tests exist and the module's owner has reviewed
the agent's first changes.

## When It Applies

It applies where there is no test coverage and no reliable account of intended behaviour. Wada's argument is that having As-Is tests alone lets a team detect defects and behaviour changes introduced by adding features, which is a large advance on having nothing — and that for an organization without the capacity for more, the value as a coverage-raising tool is already substantial.

Its limit is in what it captures. A characterization test records only how the code runs today; what the system ought to do is not in it, and on Wada's account that has to come from a human building the skill to decide it, or from digging up past decisions as software archaeology. He is explicit that To-Be tests remain the ideal and that this is a nearer goal rather than a substitute for them.

Osmani names a failure specific to letting an agent produce them: when an agent is the one making the
tests pass, the same session should not be the only author of the tests, or "you get a green suite
that encodes the implementation you just invented." His advice is to pin the behaviour first, in a
separate pass or by a person, and only then let the agent work. Where a surface has no honest unit
suite to pin, he points to running the old and new paths side by side on real or replayed traffic
and comparing their outputs instead.

## Related Terms

[[DefinedTerm/red-green-tdd]], [[DefinedTerm/test-design]], [[DefinedTerm/test-list]]
