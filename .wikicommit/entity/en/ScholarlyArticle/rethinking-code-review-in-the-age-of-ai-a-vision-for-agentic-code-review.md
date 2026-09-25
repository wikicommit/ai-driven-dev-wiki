---
title: "Rethinking Code Review in the Age of AI: A Vision for Agentic Code Review"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, agents, human-ai-collaboration]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.17548'
    hash: sha256:becc2ac1a59aad4f9155e8968fd738e02ecb7dbf2e77a818df204daa4dfd3310
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A vision paper arguing that code review effectiveness must be treated as an outcome of the whole pull-request lifecycle, and proposing a five-stage framework in which specialized LLM agents carry context between stages while humans keep control at key decision points."
  author: ["Hüseyin Özgür Kamalı", "Erdem Tuna", "Vahid Haratian", "Eray Tüzün"]
  abstract: "Code review remains a largely manual and cognitively demanding process, and AI coding assistants, by increasing code production velocity, expand the volume of code requiring review and turn review into a growing bottleneck. Current AI support is fragmented across isolated tasks such as reviewer recommendation, PR description generation or comment suggestion. The paper reviews the history of code review, identifies challenges of traditional review systems, examines the shift driven by LLMs and agentic AI, and presents a vision of an AI-powered review workflow spanning PR Creation, PR Augmentation, Reviewer Selection, AI-Assisted Code Review and PR Retrospective, with humans retained at key decision points. It then identifies open challenges and a research agenda for responsible adoption."
  keywords: ["Code Review", "AI-Driven Software Engineering", "Large Language Models", "Agentic AI", "Multi-Agent Systems", "Pull Requests", "Automated Code Review", "PR-Issue Alignment", "Change Impact Analysis", "Human-in-the-Loop"]
---

This vision paper, by authors at Ankara University, Microsoft and Bilkent University, starts from
the observation that AI coding assistants speed up code production while the review pipeline that
code must pass through has stayed largely unchanged. It argues that, under these conditions, code
review is no longer only a productivity bottleneck but the primary control surface for the quality
and accountability of AI-produced code, and that prior work improving individual review stages does not compose into effective review on
its own, because the stages depend on context that crosses tool boundaries.

The paper first traces code review through five eras defined by practice: ad hoc review
(1940s–1960s), formal inspection (1970s–1990s), lightweight peer review (1990s–2000s), integrated
code review (2000s–2010s) and automation-assisted review (2010s–2020s). It then models the
traditional pull-request workflow and groups its challenges into four areas — PR creation (missing
context, missing documentation, missing issue links), reviewer assignment, code review itself
(change understanding, change impact, [[DefinedTerm/pr-issue-alignment]], large diffs, time
pressure) and comment provision (usefulness, sentiment and toxicity) — linking several of them to
the [[DefinedTerm/lgtm-smell]].

Its proposal is an AI-powered code review framework of five stages, each combining LLM agents or
conventional tools with explicit human-in-the-loop quality gates, followed by a discussion of risks
and implications for practitioners and researchers.

## Key Points

- The paper's three stated contributions are that AI-accelerated code production amplifies rather
  than mitigates the shortcomings of PR-based review, that stage-scoped improvements cannot by
  themselves produce effective review across the lifecycle, and a five-stage framework that
  operationalizes treating review effectiveness as a lifecycle outcome.
- PR Creation: agents generate the PR title and description, link or create issues, run an
  automated first-pass review and suggest fixes, and the author interactively revises the draft
  before submitting it — a mandatory human verification step.
- PR Augmentation: four analysis agents run concurrently — alignment analysis, bug-proneness
  analysis, runtime analysis in a sandbox, and change impact analysis — and a summary agent
  synthesizes their structured findings into claims paired with evidence references and confidence
  indicators, surfacing contradictions rather than resolving them silently.
- Reviewer Selection uses conventional reviewer recommendation techniques rather than LLMs, which
  the authors justify by the balance of computational efficiency and token cost.
- AI-Assisted Code Review centres on a PR Review Agent that reviewers address in natural language,
  and on a "diff-map" that organizes changes around logical units such as functions and classes, with
  each unit anchored to the analysis reports about it; the stage also includes explanation,
  automated review, fix suggestion, toxicity measurement and usefulness measurement agents.
- PR Retrospective generates review summaries intended for both humans and later machine retrieval,
  and computes review metrics for continuous process improvement.
- In the proposed workflow, final merge authority stays with human reviewers, and the authors
  describe reviewers as moving from manual inspectors to supervisory operators of agents.
- The discussion names risks including hallucination and context degradation, limited
  generalization across projects, error accumulation across agents, evaluation difficulty,
  transparency, accountability, privacy, [[DefinedTerm/automation-bias]], deterioration of knowledge
  sharing and implicit mentoring, and hidden economic costs from cascading agent errors, for which it
  suggests confidence-based circuit breakers.

## Notes

The framework is a proposal rather than an implemented or evaluated system; the paper offers a
research agenda instead of results. For practitioners it recommends modular, incremental adoption
rather than deploying every agent at once, and treating the framework as an internal platform, and
it floats dynamic risk-based review routing ("fast lanes" and "high-risk lanes") as a possible
future extension while warning that misclassification is its main danger. For researchers it calls
for redefining review quality for hybrid human–AI settings, stratifying evaluations by review
comment type, studying interface design for AI-assisted review, context enrichment, and evaluation
metrics that capture review depth rather than speed. The paper's title uses the term
[[DefinedTerm/agentic-code-review]] for this vision of review.
