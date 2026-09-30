---
title: "Maintainability sensors for coding agents"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, coding-agents, verification, code-quality]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/sensors-for-coding-agents.html'
    hash: sha256:f44d1ed873c9fc6ebc9d49f6d0ade56e0951706724aeb8b70a4d63de4064e2da
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A May 2026 article by Birgitta Böckeler on martinfowler.com reporting her experience using computational and inferential sensors — linting, dependency rules, coupling metrics, an LLM modularity review and mutation testing — to keep an AI-built codebase maintainable."
  author: ["Birgitta Böckeler"]
  datePublished: "2026-05-27"
  publisher: "martinfowler.com"
---

This article is a practical follow-up to the author's earlier
[[BlogPosting/harness-engineering-for-coding-agent-users]], which laid out a mental model of a coding
agent harness as a system of [[DefinedTerm/guides-and-sensors]]. Here she reports her experience with
sensors that help keep a codebase maintainable — which she defines as making it easy and low risk to
change the codebase over time, also known as internal quality — on an internal analytics dashboard
(TypeScript, Next.js and React) that she rebuilt from scratch with AI, deliberately with hardly any
guides in place, to see how far sensor feedback alone would go.

The sensors she set up span the path to production: computational sensors running alongside the agent
during the coding session (type checker, ESLint, Semgrep, dependency-cruiser, test results with
coverage, incremental mutation testing, and GitLeaks in a pre-commit hook), the same sensors again in
the CI pipeline, and slower-cadence sensors run repeatedly to detect accumulated drift (inferential
security and data-handling reviews, a dependency-freshness report, and a modularity and coupling
review). The article was published in instalments between 19 and 27 May 2026.

## Key Points

- Internal quality problems affect AI agents much as they affect human developers: in a tangled
  codebase an agent may look in the wrong place for an existing implementation, create inconsistencies
  by missing a duplicate, or need more context than a task should require.
- In the author's experience, the most low-hanging AI failure modes for static analysis are the
  maximum number of function arguments, file length, function length and cyclomatic complexity — none
  of which were active in ESLint's default preset.
- She rewrote lint messages through a custom ESLint formatter into self-correction guidance for the
  agent — "a good kind of prompt injection" — allowing it to suppress a warning with a stated reason or
  slightly raise a threshold rather than forcing a binary suppress-or-comply choice. The one category
  where the agent habitually raised the threshold was the one for which she had written no such
  guidance, which she takes as an indicator that the custom messages make a difference.
- Reviewing the exceptions the AI created (suppressed warnings, raised thresholds) was a good place to
  start code review. She sees static analysis becoming more worthwhile because AI lowers the cost of
  writing custom rules and scripts, while worrying about a false sense of security and about feedback
  overload driving the agent into over-engineered refactorings.
- dependency-cruiser rules enforcing a layered module structure, with error messages expanded into
  guidance, helped the agent clean up and then keep the structure; she found this a useful replacement
  for describing code structure in a Markdown guide, though such tools only see what is expressible
  through imports, file names and folder structure.
- Coupling metrics produced by a custom tool were tedious for a human to interpret and, handed to an LLM
  (Claude Opus 4.7) on their own, gave lackluster findings that flagged deliberate patterns as problems.
  In her small experiment the data was not useful to AI by itself; she suggests it may be more useful
  for risk triage in code review, showing the impact radius of a change.
- A fully inferential modularity review using Vlad Khononov's "Modularity Skills" proved much more
  fruitful, finding duplicated route code, inconsistent ways of calling the backend, request parameters
  repeated at every level, and authentication code in the wrong place. A second run surfaced an issue
  the first had not, which she takes as a reminder to run LLM-based analysis more than once when it
  matters. She concludes that without such reviews or human coupling expertise the agent had been
  compounding inadvertent technical debt.
- Treating the test suite as a regression sensor, coverage alone was a poor indicator of test
  effectiveness: a file with 100% statement coverage and no unit tests showed 13 surviving mutants under
  Stryker because a large acceptance test executed it without verifying its effect. She calls mutation
  testing crucial once most testing is left to AI, while noting it is resource-intensive and that
  whether AI-written tests assert the right behaviour is a separate question.
- Her overall conclusion: computational sensors impressed her most at the file and function level,
  while cross-file concerns such as modularity and coupling needed an inferential sensor's semantic
  interpretation. She suspects conflicts between sensors will become an issue, having seen length rules
  push complexity into long chains of component properties.
- An appendix describes the "sidecar" CLI she vibe-coded to run all computational sensors continuously
  and give the agent a token-efficient, guidance-enriched summary. Getting the agent to check it via a
  guide (a skill or an AGENTS.md section) was easy but unreliable; hooks, git pre-commit hooks or a
  custom harness extension are the alternatives she discusses. Logging sensor history is her proposed
  way to judge a sensor's effectiveness, for instance by spotting sensors that never fail.

## Context

The article reports one practitioner's experiments on a single application, with the author stating
that her perspective is mainly that of application development such as digital products and enterprise
software, and that risk profiles vary with the kind of software built. Several findings are explicitly
provisional — the coupling-data conclusion rests on "this small experiment", and she had not yet
observed how well AI decides between conflicting rules. She leaves open how guides and sensors should
be balanced once a set of sensors is trusted, and stresses that the sensors improved her review
experience and trust without taking the human out of the loop.
