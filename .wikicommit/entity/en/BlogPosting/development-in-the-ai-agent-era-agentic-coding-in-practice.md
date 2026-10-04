---
title: "AIエージェント時代の開発 — エージェンティックコーディング実践"
type: "schema:BlogPosting"
lang: en
tags: [agents, context-files, code-review, permissions]
sources:
  - type: url
    url: 'https://zenn.dev/snowcode/articles/agentic-coding-practice-guide'
    hash: sha256:c352f7d8e6653650712d40f6de89d142c8b85d47afe73342d81497e176ccbb84
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A short practitioner's guide to agentic coding as of 2026: what changed when AI moved from autocompletion to delegated implementation, three principles for delegating well, and why diff review and permission management become the main safeguards."
  author: ["雪符しき"]
  datePublished: "2026-07-30"
---

This post describes the change in how developers work with AI as a move from "completion" to
"delegation": instead of suggesting the next lines in an editor, a coding agent now takes an
instruction, makes a plan, reads the relevant files, edits several of them, runs the tests and fixes
its own failures. It frames the resulting practice as [[DefinedTerm/agentic-coding]] and argues that
the human role is shifting from writing code to setting direction and reviewing what the agent
produces.

The bulk of the post is three principles for delegating implementation work, followed by two areas
the author treats as becoming more important rather than less once an agent writes most of the code:
reviewing its diffs, and limiting what it is permitted to do.

## Key Points

- The post proposes viewing an agent as "model plus harness": the same model can be much more or
  less useful depending on the surrounding machinery for file operations, test execution and
  permission management (see [[DefinedTerm/agent-harness]]).
- Its survey of tools as of 2026 — [[SoftwareApplication/claude-code]], [[SoftwareApplication/openai-codex]],
  [[SoftwareApplication/cursor]], [[SoftwareApplication/github-copilot]] and [[SoftwareApplication/cline]] —
  concludes that each has trade-offs and that the practical answer is to choose by workflow.
- First principle: split work into pieces a human can review. Delegating large tasks feels faster, the
  post argues, but a diff too large to review ends up as rework.
- Second principle: give the agent a means of verification before it starts, such as the test command
  to pass, so that it can judge success itself and iterate; the author states that "build, let the agent
  test itself, then review" runs far faster than "build, have a human try it, then ask for fixes".
- Third principle: provide context through files in the repository. The post describes
  [[DefinedTerm/agents-md]] as a tool-independent convention read by several agents and
  [[DefinedTerm/claude-md]] as the file Claude Code reads, and recommends recording project layout,
  conventions, commands and prohibitions there; it notes that layering these files from home directory
  to project root to subdirectory is common practice.
- Because agents generate code quickly and in volume, the post treats reading every diff as the core
  of quality: rejecting unintended or excessive changes, asking why an implementation was chosen
  rather than accepting it because it runs, and keeping tasks small on the assumption that review will
  become the bottleneck (compare [[DefinedTerm/review-bottleneck]]).
- On security it recommends least privilege with permission required for destructive commands, keeping
  API keys and passwords out of prompts and repositories, and instructing the agent not to follow
  instructions found in external documents or web pages it reads, as a precaution against
  [[DefinedTerm/prompt-injection]].

## Context

The post is a general, introductory overview written from the author's own practice rather than a
report of measured results; its recommendations are presented as an individual practitioner's
summary of the state of things in 2026, and its tool characterizations are one-line impressions.
