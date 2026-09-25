---
title: "Verification loop"
type: "schema:DefinedTerm"
lang: en
tags: [verification, agentic-coding]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/coding-agents-manager/'
    hash: sha256:fc697c3fcc830075a1a6b6751a1f242d4b6ff4ea9a385c1ec60a0c6f8a6e50a1
  - type: url
    url: 'https://blog.langchain.com/improving-deep-agents-with-harness-engineering/'
    hash: sha256:7628e7920b4c219963d45c07cb27a6039a14ef5a60f3939b0ccb424dd7481ddd
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A required cycle of automated checks and structured reporting — running tests, linting, and, optionally, a second agent's review — built into how an AI coding agent's own output is checked before a human reviews it."
---

A verification loop is a set of required checks built into how an AI coding agent's work is validated before a human reviews the result, so that low-quality output is caught early rather than discovered late. The term is used this way in a post by Addy Osmani on managing coding agents, which is where the practical checklist below comes from.

## Usage

Addy Osmani describes a verification loop in practice as requiring the agent to run the test suite (or a scoped subset) and include the output in its final message, requiring lint and typecheck to pass for touched areas, requiring the agent to add or modify tests for behavior changes, and requiring a structured "PR packet" at the end — a summary of changes, the reasoning behind the approach, the files touched, the test plan plus results, and any risks or follow-ups. He also describes a two-agent pattern, which he ties to [[Organization/anthropic]]'s published guidance for [[SoftwareApplication/claude-code]], treating the work as a two-person workflow with separation of concerns: Agent A implements, Agent B reviews for correctness, style, edge cases, and missed tests, and then Agent A — or a fresh Agent C — applies the review feedback and re-runs verification.

## When It Applies

Verification loops matter wherever work is delegated to an agent that can generate large volumes of output quickly, since agents are described as able to generate low-quality work at high speed, the same way reviewing low-quality human work too late wastes time. The practice assumes a test suite, linter, and typechecker that can be run in scope, and a way for the agent to report its results in its final message. Osmani also describes OpenAI's Codex as taking an explicit stance on tool use in the same spirit: running commands and tests and iterating to a passing state before proposing a pull request.

A LangChain post on harness engineering, [[BlogPosting/improving-deep-agents-with-harness-engineering]],
describes the same idea from the harness side, as a build-verify loop through which an agent improves via
feedback within a single run. Its observation is that models do not enter such a loop on their own: the
most common failure in its traces was an agent that wrote a solution, re-read its own code, judged it fine
and stopped. The team added system-prompt guidance for a four-step cycle — plan (including how the
solution will be verified), build (writing tests for happy paths and edge cases), verify (running the
tests and comparing the result with what was asked rather than with the agent's own code), and fix — and a
middleware that intercepts the agent before it exits to remind it to verify against the task
specification. It argues that this matters most in autonomous systems with no human in the loop, since
models are biased toward their first plausible solution.

## Related Terms

[[DefinedTerm/agent-teams]], [[SoftwareApplication/claude-code]], [[DefinedTerm/ralph-loop]], [[DefinedTerm/doom-loop]]
