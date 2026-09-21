---
title: "Test List"
type: "schema:DefinedTerm"
lang: en
tags: [tdd, ai-assisted-programming]
sources:
  - type: url
    url: 'https://future-architect.github.io/articles/20260619a/'
    hash: sha256:69f4f7ee90c148297c70f911f5ac57d2d6c405c2b3e2660661065679a91f7da9
  - type: url
    url: 'https://agilejourney.uzabase.com/entry/2025/08/29/103000'
    hash: sha256:3ddb48b38b85526ba30bc0c2f6e032f2041384360d5a6e24c4261f8581fefe0d
    license: all-rights-reserved
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The set of test cases fixed at the start of a test-driven development cycle, naming which behaviours are to be made to work and in what order. In agentic coding it is the step that still requires human hands — the developer frames and slices it and reviews what comes back, even though the agent drafts the cases themselves."
---

A test list is the set of test cases settled at the start of a test-driven development cycle,
before the implementation exists — a record of which behaviours are to be made to work, and in what
order. [[BlogPosting/making-ai-do-t-wada-style-tdd]] calls it the first step of TDD and the one
that still needs human hands if the rest is to be delegated to an agent, and quotes a passage
arguing that many readers miss this first step, so that the complaint that TDD starts writing code
immediately with no view of when it will end is wide of the mark. Tsutomu Yasui, in
[[BlogPosting/tdd-as-guardrail-in-the-age-of-ai-agents]], attributes the device to Kent Beck.

## Usage

In agentic coding the list is where the work is divided rather than where it is written out by
hand. On that account the developer verbalises the feature the session is meant to produce, which
amounts to the coarse external-integration case; the agent is then made to produce the
unit-level and internal-integration cases that replace that outline with the behaviour of specific
functions. The developer also decides in advance where the slices fall — initial data retrieval,
input and submission are the units given for the tool described — which is what makes the
decomposition go smoothly.

Control is retained by reviewing what comes back rather than by writing it. The list can be checked
in the agent's plan mode when proceeding carefully, or watched as it scrolls past in an automatic
mode and interrupted with Esc, sometimes rewinding the session history, when it heads somewhere
unintended.

Yasui makes a related but distinct case for letting a model draft one: that writing a test list is
harder than it looks, because a large "what I want to do" has to be broken down into pieces fine
enough for a program to verify, and asking a model for a test list does yield something of the
sort. He grants the objection — TDD uses the list as a guide for the developer's own thinking, so
there is a real question about not writing it yourself — but argues the effect is to lower the
barrier to entering TDD at all, by making visible how a problem can be decomposed and where to
start. He adds that models are good at taking one written case and extending it toward coverage.

## When It Applies

It applies where an agent is to carry out a change on its own and the result has to be verifiable
rather than merely plausible. What the cycle can deliver is that something not working now comes to
work and stays working; which behaviours are chosen, and in what order, is the selection the cycle
itself does not make. It assumes the developer knows the domain well enough to make that selection
— the same account argues this is where domain knowledge now pays off, since being able to have a
good list produced accurately from the outset is what makes the agent's start fast. Yasui draws the
boundary in the same place from the other direction: which tests ought to be added is a separate
question, settled through [[DefinedTerm/test-design]] rather than by whatever the model produced.

It is misapplied when the drafted list is left unreviewed. The account gives the example of a
request for weekly batch submission where the agent was heading toward making the daily input
screen weekly as well, until it was interrupted and told to keep input per day and batch only the
submission. For changes to existing behaviour the list is also incomplete on its own: existing
tests guarantee only what is not meant to change, so the intended new behaviour has to be supplied
alongside it or the agent breaks more than intended. And satisfying the list is not the same as
satisfying it honestly — where a change degrades many existing tests at once, the agent may hack
them back to green, which is why an unexpectedly large diff is audited from a separate, clean
session rather than trusted.

As evidence this is one practitioner's report of personal tooling, published on their employer's
engineering blog, with most of the trial and error described dating from around March. Its use as
the human-retained step when delegating to an agent is offered as the author's own working practice
rather than a measured result. Yasui's account of using a model to draft the list is likewise
offered as his own experience, and he is explicit that he does not treat it as unambiguously good.

## Related Terms

[[DefinedTerm/red-green-tdd]], [[DefinedTerm/non-delegation-zone]], [[DefinedTerm/vibe-coding]],
[[DefinedTerm/human-in-the-loop]], [[DefinedTerm/test-design]], [[DefinedTerm/characterization-test]]
