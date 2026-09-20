---
title: "AI writes code faster. Your job is still to prove it works."
type: "schema:BlogPosting"
lang: en
tags: [code-review, ai-assisted-programming, verification, human-oversight]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/code-review-ai/'
    hash: sha256:e678c0f13766adc73b4d03c644a747b3d135be132242e1875d32cfbf38e936be
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A January 2026 post arguing that AI did not kill code review but made the burden of proof explicit: changes should ship with evidence that they work, and review should then be spent on risk, intent and accountability. It contrasts how solo developers and teams absorb AI-speed output and sets out a PR Contract authors owe reviewers."
  author: ["Addy Osmani"]
  datePublished: "2026-01-07"
---

This post argues that AI has not made code review obsolete but has made the burden of proof
explicit. Its opening claim is that a pull request without evidence that it works is not shipping
faster — it is moving work downstream. From there it separates two things that AI speed tends to
collapse together: producing a change, and establishing that the change does what it is supposed to
do. Osmani restates a rule he says he has made before — if you have not seen the code do the right
thing yourself, it does not work — and argues that AI amplifies that rule rather than excusing it.

The post splits the question by working context. Solo developers, it says, increasingly ship at
"inference speed", reviewing only key parts and leaning on automated tests as the backstop; teams,
where the cost of mistakes and the longevity of the code are higher, use AI review bots for a first
pass but keep human sign-off. Both patterns, on the post's account, treat AI as an accelerator, and
what distinguishes them is verification — who does it, what it covers, and when it happens.

Its practical output is a short framework, the [[DefinedTerm/pr-contract]], for what an author owes
a reviewer, together with a set of principles for how human and AI review divide the work. The
closing framing is that the bottleneck has moved from writing code to proving it works, and that the
human remains responsible for whatever the AI delivers.

## Key Points

- The post's central claim is that AI did not eliminate code review; it made the burden of proof explicit, so changes should ship with evidence such as passing tests and manual verification, and review should then be spent on risk, intent and accountability.
- Osmani argues that skipping review does not remove work but defers it, and that developers who succeed at high velocity with AI are the ones who built verification systems first.
- For solo developers the post recommends extensive automated testing as a safety net, language-independent and data-driven tests so an agent can build or fix implementations in any language while verifying as it goes, and continued manual testing and critical reasoning on the finished product. Osmani describes his own loop as drafting a spec.md with the AI, approving it, then iterating write → test → fix.
- For teams the post's claim is that the practical problem is volume rather than missed style issues: AI increases output faster than verification capacity, which makes review the rate limiter, so teams should enforce incrementalism and break agent output into digestible commits.
- Security is named as the area where human oversight is non-negotiable; the post's rule is that code touching auth, payments, secrets or untrusted input requires a human threat-model review plus a security tool pass before merge.
- Code review is presented as a knowledge-transfer mechanism: when an author cannot explain AI-generated code they submitted, the post argues the team loses the shared context that makes on-call debugging possible.
- The post reports that experience with AI review tools is mixed — valuable when tuned, dismissed as "text noise" when not — and concludes that such tools require deliberate configuration of sensitivity, comment types and opt-in policy.
- Human accountability is stated as a hard line: however much AI contributed, a human must take responsibility for the change.

## Context

The post is written from Osmani's own vantage as a practitioner and draws on several kinds of
outside material, which it links rather than reproduces: survey figures on how much senior
developers now ship AI-generated code, reported error and security-flaw rates in AI-generated code,
measurements of pull-request size and change-failure rates under AI adoption, and published
positions from other practitioners. Two of those are quoted directly and belong to their authors
rather than to the post: Peter Steinberger's account of no longer reading much code, watching the
stream and looking only at key parts, and Greg Foster of Graphite saying he does not see AI agents
becoming a stand-in for a human engineer signing off on a pull request. The post also points to the
OCaml maintainers' rejection of a 13,000-line AI-generated pull request as an illustration that
reviewing AI-generated code is more taxing than reviewing human code, and that volume itself is the
problem teams must manage.

Looking ahead, the post expects growing emphasis on AI governance in larger organisations —
formalised policies about AI contributions, sign-offs that an employee reviewed the code, roles such
as "AI code auditor", and enterprise platforms offering multi-repository context and custom policy
enforcement. Its stated view is that these are changes in how review happens, not in what review is
for.
