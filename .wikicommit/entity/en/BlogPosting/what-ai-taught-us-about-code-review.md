---
title: "AIが教えてくれたコードレビューの本質　― 意図共有という学び ―"
type: "schema:BlogPosting"
lang: en
tags: [code-review, ai-adoption, human-in-the-loop]
sources:
  - type: url
    url: 'https://developersblog.dmm.com/entry/2025/12/02/110000'
    hash: sha256:fd805ea09ceea62557093852cd7e6e52043a461198208dca231e0465b7254161
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A post from DMM's User Review Group reporting that an AI pull-request auto-approval system worked technically but never took root in the team, and arguing that what the automation removed was code review's function as a dialogue for sharing intent."
  author: ["松井"]
  datePublished: "2025-12-02"
  publisher: "[[Organization/dmm]]"
---

This post is an account of an automation that worked and was not adopted. The author, writing from the User Review Group in DMM's Platform Development Division, describes building a pull-request auto-approval system on [[SoftwareApplication/claude-code-action]] in July 2025: the agent scored each pull request and approved it automatically when the scores cleared a threshold. The post reports that accuracy was not bad and that prompt tuning achieved stable operation — and then that the mechanism did not take hold in the team. The post treats that gap, rather than any accuracy problem, as its subject.

The explanation it reaches is that code review is not only a quality check but a dialogue in which intent is shared, and that the team's discomfort came from automating that dialogue away. The post sets this against an earlier automation by the same group that did succeed — an AI content-moderation system for user-submitted reviews — and locates the difference in the task rather than in the tooling: moderation, it says, requires no sharing of background or intent, and on that point code review was decisively different.

The conclusion is a division of labour the post presents as a two-layer table: Layer 1, code quality, is what AI is good at; Layer 2, intent and judgement, is what people are good at. The author's closing position is that pursuing AI automation alone makes a team fast in the short term but weak to change, while accumulating shared intent is slower and produces a team that is resilient — and that designing this balance is the crux of development in the AI era.

## Key Points

- The team built PR auto-approval with [[SoftwareApplication/claude-code-action]] in July 2025, having the AI reviewer score each pull request on four axes — `pr_clarity_score` (clarity of the AI's judgement), `code_quality_score`, `test_quality_score` and `security_quality_score` — and set `auto_approval` to `"Y"` only when the scores met the criteria. The post shows a sample output object carrying those four scores alongside a PR summary and a stated reason.
- Accuracy was acceptable and prompt adjustment produced stable operation, but the mechanism did not become established in the team. The post presents this as its central puzzle: the failure was in adoption, not in the model.
- Code review is described as a dialogue that shares intent, not only a quality check. The post gives two illustrative exchanges — one where a reviewer asks why an implementation was chosen and the answer is that a rushed release led the author to take the safe option, and one where reading a pull request tells the next engineer that a later feature can be built by extending or inheriting from what was just added. The first is characterized as sharing the background to a judgement and as what builds team trust; the second as intent-sharing at the code level and a bridge to the next design.
- The same group had already automated a different task completely: an AI content-moderation system that analyses submitted user reviews and judges prohibited terms and rule violations, reported as auto-approving over 60% of all reviews and cutting approval time from one to three days down to about ten minutes. The post's argument turns on this contrast — moderation requires no sharing of background or intent, and that is stated as the decisive difference from code review.
- AI-generated code is described as tidy and passing its tests while not conveying why it was done that way. The post allows that an AI can generate reasons, but says it cannot express hesitation, comparison, or wavering in judgement — so an AI-authored pull request may work correctly without being trustworthy, and this "layer of trust" is named as the part people should carry.
- The post's summary model splits review into Layer 1, code quality, assigned to AI as its strength, and Layer 2, intent and judgement, assigned to people. Pure code-quality checking is stated as delegable to AI; the time spent sharing intent and deepening understanding is stated as the part people should own.
- Everything above is one team's account of its own experience, offered without measurement of the adoption failure it describes.

## Context

The post places itself inside an AX (AI Transformation) strategy being pursued in DMM's Platform Development Division, and says the group promotes AI-driven productivity improvement through practices such as weekly AI analysis meetings and the use of Findy Team+. Against that background it reports that the team felt a wall of its own, and that it set out to re-examine the causes by way of code-review automation.

The author frames the automation's cost in terms of what a team loses rather than what it gains: if code is generated in volume and the discussion of why it was written that way is cut, the codebase stops growing as living knowledge and the team becomes weak to change. The post closes by putting the design question back to the reader rather than prescribing a configuration.
