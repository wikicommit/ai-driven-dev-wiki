---
title: "PR Contract"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, verification, ai-assisted-programming]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/code-review-ai/'
    hash: sha256:e678c0f13766adc73b4d03c644a747b3d135be132242e1875d32cfbf38e936be
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A four-item framework for what the author of a pull request owes its reviewer - intent, proof that the change works, the risk tier and which parts were AI-generated, and the one or two areas where human input is wanted."
---

The PR Contract is a short framework, set out in
[[BlogPosting/ai-writes-code-faster-your-job-is-still-to-prove-it-works]], for what the author of a
pull request owes the person reviewing it. It has four items: **what/why**, the intent of the change
in one or two sentences; **proof it works**, meaning tests passed and manual steps such as
screenshots or logs; **risk and AI role**, naming the risk tier and which parts of the change were
AI-generated; and **review focus**, one or two areas where human input is specifically wanted.

Osmani presents it not as process overhead but as respect for reviewer time and as a forcing
function for author accountability, with the test stated plainly: an author who cannot fill the
contract out does not understand their own change well enough to ask someone else to approve it.

## Usage

The contract is the author-side half of a division of labour the same post describes for review
under AI speed. Its companion principles are to insist on proof rather than promises — no pull
request goes up without either new tests or a demonstration of the change working, and AI agents
should be prompted to execute code or run unit tests after generating it; to treat AI review output
as advisory, a first-pass reviewer rather than the final arbiter, described as spellcheck rather than
an editor; to point human review at what AI misses, such as security holes, duplication of existing
code and maintainability of the approach; to enforce incremental development in small commits with
clear messages, never committing code the author cannot explain; and to maintain high testing
standards, using AI to draft edge-case tests.

These sit inside the post's wider framing: that AI shifted the bottleneck from writing code to
proving it works, and that a pull request without evidence that it works does not ship faster but
moves work downstream.

## When It Applies

The contract is written for changes where a human other than the author will review the work, and it
assumes both that tests or a reproducible manual demonstration are available to attach and that
someone is empowered to withhold approval when they are not. It is presented as applying whether the
developer is working solo or on a team, although the post's account of *why* differs between the
two: solo developers use it against their own velocity, teams against the volume AI adds to the
review queue. Its stated failure mode is on the author's side: an author who cannot complete the
four items does not understand their own change well enough to ask someone else to approve it.

On the question of how well established it is: the post describes this as a framework the most
successful teams have converged on and as an emerging best practice, but it is presented in one
practitioner's post rather than backed by a study, and the wording of the four items is that post's
own.

## Related Terms

[[DefinedTerm/merge-readiness-pack]], [[DefinedTerm/review-bottleneck]],
[[DefinedTerm/verification-debt]], [[DefinedTerm/code-review-agent]]
