---
title: "Supervisory Engineering Work"
type: "schema:DefinedTerm"
lang: en
aliases: ["Supervisory Engineering"]
tags: [human-oversight, developer-experience, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.23135'
    hash: sha256:3e017ddd415719f2210ad1a5afb381f4f70a87438df16f7b32b5c7121db023a7
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A proposed category of software engineering work, encompassing the effort of directing an AI coding assistant, evaluating its output and correcting its errors, which its proposers argue traditional software development lifecycle task categories do not capture."
---

Supervisory engineering work is a category of work proposed by Annie Vella and Kelly Blincoe in
[[ScholarlyArticle/impact-of-ai-coding-assistants-on-software-engineering]] to describe the effort
software engineers spend directing AI coding assistants, evaluating what they produce and correcting
their errors. The authors present it as a new, distinct category that traditional software
development lifecycle (SDLC) taxonomies — designing, coding, testing, reviewing — do not capture, and
as a possible explanation of where perceived time savings from traditional tasks are being
reallocated.

## Usage

The construct emerged in that study from convergent quantitative and qualitative patterns.
Engineers reported spending less time on most development tasks, with writing code showing the
steepest decline, yet verification tasks such as testing and code review rose only modestly, which
raised the question of where the effort was going. In open-ended responses participants described
shifting from producing code to supervising AI-generated output — directing the assistant,
evaluating its suggestions and deciding what to accept, modify or discard — work that does not map
cleanly onto existing task categories. The authors suggest that engineers may not recognise this
verification of AI output as "testing" or "code review" in the traditional sense.

They break it into three components:

- **Directing** — specifying intent, crafting prompts, providing context, and iterating when output
  misses the mark.
- **Evaluating** — reading AI output and deciding what to accept, modify or reject.
- **Correcting** — fixing errors, integrating output into existing code, and maintaining consistency.

How much supervision an engineer performs depends, in the authors' account, on trust calibration:
engineers vary in how readily they accept AI output, with some restricting AI to low-risk contexts.
They also link the construct to their [[DefinedTerm/productivity-experience-paradox]]: the cycle of
prompting, reviewing, accepting or rejecting and iterating replaces sustained focus with a rhythm
of directing, waiting and evaluating, which they suggest may help explain why flow state eroded.

The concept is at the proposal stage. It rests on one longitudinal survey study, and its authors
list as future work testing whether supervisory engineering work is empirically distinct from
existing activities, what skills it requires, and whether engineers find it satisfying; if it
proves real and distinct, they suggest SDLC models may need updating.

## Related Terms

- [[DefinedTerm/creation-to-verification-shift]]
- [[DefinedTerm/productivity-experience-paradox]]
- [[DefinedTerm/human-in-the-loop]]
- [[DefinedTerm/verification-debt]]
