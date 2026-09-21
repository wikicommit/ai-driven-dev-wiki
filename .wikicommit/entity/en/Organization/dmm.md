---
title: "DMM"
type: "schema:Organization"
lang: en
tags: [ai-adoption, industry]
sources:
  - type: url
    url: 'https://developersblog.dmm.com/entry/2025/12/02/110000'
    hash: sha256:fd805ea09ceea62557093852cd7e6e52043a461198208dca231e0465b7254161
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A company whose Platform Development Division is advancing an AX (AI Transformation) strategy, and across which, according to one of its engineering groups, AI-agent adoption advanced rapidly during 2025 while the load of code review rose with the volume of AI-generated code."
---

DMM appears in this wiki as an adopter of AI-driven development practice rather than as a vendor of tooling. What is recorded here comes from a post on the company's own developers' blog, written from inside one group, so it establishes how that group describes its organization rather than an outside assessment of it.

The organization-level condition the post reports is that 2025 was a year in which AI-agent adoption advanced rapidly across DMM as a whole, and that code generation by AI agents increased, with the load of code review rising sharply as a result. That rise is given as the reason the group took on review automation at all.

## Background

The post situates its work inside an AX (AI Transformation) strategy being advanced in DMM's Platform Development Division. It describes the author's own group as promoting AI-assisted productivity improvement and as having worked to root a culture of AI use through practices including weekly AI analysis meetings and the use of Findy Team+.

The post also reports that the group felt a wall in turning AI adoption into productivity, and that it re-examined the causes by way of code-review automation.

## Activities & Products

The group the post is written from — the User Review Group (URG) — develops the system that processes user-submitted reviews on DMM, and the post describes its platform as under constant demand to hold quality and speed together.

Two AI systems built by that group are described, at different stages of maturity. The first is an automatic-approval system for content moderation, in which AI analyses submitted reviews and judges prohibited terms and rule violations; the post reports it running in production, auto-approving over 60% of all reviews without human involvement and reducing approval time from one to three days to roughly ten minutes. The second is a pull-request auto-approval mechanism built on [[SoftwareApplication/claude-code-action]] in July 2025, which the post reports as technically workable but never established within the team — the account of that outcome is on [[BlogPosting/what-ai-taught-us-about-code-review]].
