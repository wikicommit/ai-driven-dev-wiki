---
title: "用Agent评测思路管理AI Coding —— 31万行代码AI重构的实践"
type: "schema:BlogPosting"
lang: en
tags: [ai-coding, refactoring, technical-debt, code-review, coding-standards]
sources:
  - type: url
    url: 'https://tech.meituan.com/2026/05/07/Agent-AI-Coding.html'
    hash: sha256:6c4f31a31d435754bd5f5c122013b52a505853527f84f233066089ac7f29a2e8
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Meituan technical-team post on refactoring a 310,000-line agent-evaluation system, over 90% of whose code is AI-generated, without pausing business delivery — arguing that AI coding should be managed the way agents are evaluated: align people first, then align the AI."
  author: ["业务研发平台"]
  datePublished: "2026-05-07"
  publisher: "美团技术团队 (Meituan technical team)"
---

This post from the Meituan technical team's blog, published on 2026-05-07 under the byline
业务研发平台, is a firsthand account of refactoring an agent-evaluation system that had grown from
under 50,000 lines of code in June 2025 to 310,000 lines, at an average of 16 requirements a month,
while more than 90% of the team's code was being written with AI. Its starting observation is that
AI coding does not converge complexity on its own: without a shared standard, code written with AI
by different people diverges in style and the system decays faster, not slower.

The team presents three lessons from doing the refactor without stopping business delivery. First,
that managing AI coding follows the same logic as the agent evaluation the team works on — first
align people with each other on a standard ("人人对齐"), then turn that consensus into constraints the
AI executes ("人机对齐"). Second, that AI is redrawing the value of experience: engineers using AI
found ten deeply hidden performance risks in a short time, and the post argues the value of
experience is moving from being able to see the whole system to judging what matters. Third, that
technical debt can be absorbed iteratively, like business requirements.

## Key Points

- The team frames its method as a reuse of its evaluation practice: first "people-to-people
  alignment" on standards, then "human-machine alignment" by constraining the model with AI Rules
  and Skills. This is the team's own framing, drawn from its own experience.
- The post argues the order matters: without team consensus first, even well-written AI Rules are
  interpreted differently by different people; in its words, the bottleneck is people, not tools.
- It argues that when AI is the main source of code, coding standards stop being mainly a
  collaboration aid and become infrastructure for constraining AI output, because a model generating
  code leans heavily on the existing code patterns and amplifies inconsistency rather than correcting it.
- Technical-debt discovery used "expert direction plus AI-assisted investigation": core developers
  set the high-risk boundaries and priorities, and AI did the exhaustive scanning. The team reports
  identifying three P0 and two P1 debt items this way with limited resources.
- The team turned its standards (engineering layering, business-domain model conventions and
  repository-layer conventions) into "always"-level AI Rules applied during coding and in a
  pre-review step, and captured its agreed division of domain responsibilities as a Skill loaded
  progressively while coding.
- Migration into a four-layer structure (Starter / Application / Infrastructure / Common) was
  done entirely with AI: the refactoring lead migrated the two most complex packages personally,
  distilled the process into an SOP the AI could execute, and the rest of the team applied it to
  more than ten core packages while focusing on business-semantics acceptance and code review.
- Rather than a rewrite or a dedicated refactoring project, the team split technical debt into
  "incidental actions" attached to high-priority business requirements, and reports requesting not
  a single day of dedicated refactoring time.
- As AI shortened coding time, code review became the most congested stage — the post's
  "barrel effect" — and it argues that unless review gets faster, review swallows the productivity
  gain (see [[DefinedTerm/review-bottleneck]]).
- Its responses were a Pre-PR mechanism, in which developers run several rounds of AI self-review
  and fix everything the AI finds before submitting a PR document, a higher-tier model acting as
  judge over a lower-tier model's code, and models from different vendors reviewing each other's
  output, which the team reports gave broader review coverage in practice.
- For AI-assisted testing, where developers also act as QA on all requirements, the team found
  fully AI-generated test cases missed implicitly related high-risk scenarios and produced many
  low-value edge cases, and settled on a five-step human-in-the-loop SOP in which people set scope
  and risk level and AI scans code and fills in cases.
- The post concludes that when 90% of code is AI-generated, engineers' focus should shift from
  writing code to designing and maintaining an engineering environment in which AI produces code
  reliably.

## Context

The account is one team's experience on one internal system, and its figures (ten performance
risks, the P0/P1 counts, the growth in lines of code) are the team's own reports rather than
measured comparisons. It ends with a four-step guide for other teams: map the technical debt with
AI doing the exhaustive scan, agree standards and encode them as AI Rules and Skills, have a lead
build a reusable migration SOP, and establish a Pre-PR mechanism so that human review can focus on
business semantics.
