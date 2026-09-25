---
title: "Context-Efficient Backpressure for Coding Agents"
type: "schema:BlogPosting"
lang: en
tags: [context-engineering, coding-agents, verification]
sources:
  - type: url
    url: 'https://www.humanlayer.dev/blog/context-efficient-backpressure'
    hash: sha256:e57c7b4289eae44405b7fa2bcda631a3a903cec96d2347c19da0a422f664cbe9
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A short HumanLayer post recommending that coding agents see a single check mark for a passing test, build or lint stage and the full output only on failure, so verification output does not waste context."
  author: ["Dex"]
  datePublished: "2025-12-09"
  publisher: "HumanLayer"
---

This post describes a pattern the author says HumanLayer uses constantly: swallow all test, build and
lint output and replace it with a single `✓` when the stage passes, printing the stashed output only
when the exit code is non-zero. Its reasoning is about context rather than cost. A test run can dump
hundreds of lines the agent must parse to find the one failure it needs, and when everything passes,
2-3% of the context window has been spent on an "all good" that fits in under ten tokens. The author
urges staying inside what he calls a roughly 75k-token "smart zone" for Claude models, and argues that
human time lost wrangling an agent in the "dumb zone" is likely ten or more times more expensive than
the tokens.

The post also pushes back on recent models' own attempts to economize — swallowing output to
`/dev/null`, or piping a long test suite through `head` and then having to re-run it — which it says
end up burning more tokens, human time and mental energy. It speculates that model behaviour was tuned
this way to help in codebases whose backpressure mechanisms are not context-efficient, and concludes
that deterministic is better than non-deterministic: if you already know what matters, do not leave a
model to churn through junk tokens to decide.

## Key Points

- Take control of output deterministically instead of letting the model decide what to truncate: a
  `run_silent` shell wrapper prints `✓ <description>` on success and `✗ <description>` followed by the
  full output on failure.
- Then iterate: enable fail-fast flags (`pytest -x`, `jest --bail`, `go test -failfast`) so the agent
  handles one failure at a time; filter out generic stack frames and timing information; and add
  framework-specific parsing so test counts stay visible without the noise.
- The author reports using the pattern heavily with customers' Maven and Gradle projects and says it
  works equally for xcodebuild, cargo and other verbose tools; HumanLayer runs its monorepo checks this
  way in a pre-push hook and for each plan phase, output the post says would otherwise fill about half a
  context window.
- Once output is wrapped, the remaining job is persuading the model not to do its own truncation — for
  which the post suggests instructions in the project's CLAUDE.md (see
  [[BlogPosting/writing-a-good-claude-md]]).
- All of this is presented from the author's own practice; the token comparison it shows uses an
  unofficial tokenizer that the post itself says is probably out of date.

## Context

The post applies [[DefinedTerm/backpressure]] — the checks that push back on an agent's output — with a
context-engineering constraint: those checks should reject bad work without flooding the context
window. Related pages include [[DefinedTerm/context-engineering]], [[DefinedTerm/context-rot]] and
[[BlogPosting/skill-issue-harness-engineering-for-coding-agents]].
