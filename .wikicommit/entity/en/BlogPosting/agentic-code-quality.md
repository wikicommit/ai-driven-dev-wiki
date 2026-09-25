---
title: "Agentic Code Quality"
type: "schema:BlogPosting"
lang: en
tags: [agentic-engineering, verification, code-review]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agentic-code-quality/'
    hash: sha256:56349ced5b7fdba7ce2fa4ec5b60235f5fff08ae8eda38b2493c358817cec69f
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A post arguing that, because agents generate more code than people can read, software quality now depends on the constraints set around agents — quality gates applied as back-pressure throughout the delivery loop rather than a single human review at the end."
  author: "Addy Osmani"
  datePublished: "2026-08-08"
---

This post argues that code review — someone reading what you wrote — does not scale to agents, because there is too much code for anyone to read, so more and more quality checks have to live in the harness, environment and operating system around the agent. Its central claim is that software quality now depends on the constraints set around agents: an agent can propose anything, and the constraints decide whether a proposal is safe, correct, scoped and useful enough to ship. The author still reads and reviews code himself, but says he is deliberate about where he is comfortable letting constraints be the check.

The post calls these constraints quality gates and treats them, together with [[DefinedTerm/backpressure]], as the mechanism by which teams keep production software reliable even when agents generate very large numbers of changes. It closes by asking readers to write their own constraint-driven plan for quality.

## Key Points

- Quality gates take many forms: unit, property and acceptance tests; mutation testing; code-quality metrics such as cyclomatic complexity and line length; and checks on which change proposals the system will accept and apply.
- Using a list by Guillermo Rauch of situations where not reading code may be acceptable, the post observes that each such case is really a statement about low stakes (no users, throwaway code, a prototype); once stakes rise, something has to read the code, and if it is not a human on every diff it has to be the constraints.
- Two open issues are named: autonomy (agents may fail when information is missing or the task is ambiguous, for many of the same reasons humans fail, such as brittle environments, nondeterministic builds, missing permissions and weak tests) and trust, which the author says has to be hard-earned.
- The environment the post aims for is one where an agent can do real work, get feedback it can trust, and fail without doing much damage.
- Constraints act at different points: some shape work before it begins, some give feedback while the agent works, and some decide whether output may cross the production boundary at all.
- The author recommends a broad but intentionally chosen set of checks, each with a distinct responsibility (from type safety and performance to late-stage security scanning), rather than relying solely on unit tests; architecture rules can be enforced by linting tools such as ESLint.
- Human attention is framed as scarce: inserting a human check into a system that otherwise moves at machine speed will hurt productivity, so humans should be pulled in when automated guardrails break and directed at the nuanced problems that need judgment.
- Quality is described as a collection of signals of varying importance — correctness, maintainability, performance, security, efficiency and comprehensibility — rather than a single metric.
- When verification cannot keep up with the volume of changes, the post lists three responses: scale the verification system, slow the rate at which agents generate changes, or lower the quality bar; it also suggests relaxing constraints in some places while keeping them tight where they matter most.
- The author states that, for now, much of the difference between useful agent output and slop still comes down to the skill of the team operating the loop.

## Context

The argument is presented as the author's own view and experience rather than a measured result. The post notes that it was originally published on the author's Substack. See also [[DefinedTerm/deterministic-quality-gate]] and [[DefinedTerm/guardrails]].
