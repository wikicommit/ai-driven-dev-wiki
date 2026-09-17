---
title: "Verification loop"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/coding-agents-manager/'
    hash: sha256:fc697c3fcc830075a1a6b6751a1f242d4b6ff4ea9a385c1ec60a0c6f8a6e50a1
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A required cycle of automated checks and structured reporting — running tests, linting, and, optionally, a second agent's review — built into how an AI coding agent's own output is checked before a human reviews it."
---

A verification loop is a set of required checks built into how an AI coding agent's work is validated before a human reviews the result, so that low-quality output is caught early rather than discovered late.

## Usage

In practice this means requiring the agent to run the test suite (or a scoped subset) and include the output in its final message, requiring lint and typecheck to pass for touched areas, requiring the agent to add or modify tests for behavior changes, and requiring a structured "PR packet" at the end — a summary of changes, the reasoning behind the approach, the files touched, the test plan plus results, and any risks or follow-ups. Osmani cites [[Organization/anthropic]]'s own guidance for [[SoftwareApplication/claude-code]] as recommending running multiple instances where one writes code and another verifies it via review and tests, treating it as a two-person workflow with separation of concerns, and describes a two-agent pattern built on the same idea: Agent A implements, Agent B reviews for correctness, style, edge cases, and missed tests, and then Agent A — or a fresh Agent C — applies the review feedback and re-runs verification.

## When It Applies

Verification loops matter wherever work is delegated to an agent that can generate large volumes of output quickly, since agents are described as able to generate low-quality work at high speed, the same way reviewing low-quality human work too late wastes time. The practice assumes a test suite, linter, and typechecker that can be run in scope, and a way for the agent to report its results in its final message. Anthropic is credited with recommending the two-agent variant as a workflow upgrade, and OpenAI's Codex is described as taking an explicit stance on tool use in the same spirit: running commands and tests and iterating to a passing state before proposing a pull request.

## Related Terms

[[DefinedTerm/agent-teams]], [[SoftwareApplication/claude-code]]
