---
title: "Superpowers"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-skills, coding-agents, test-driven-development, subagents]
sources:
  - type: url
    url: 'https://github.com/obra/superpowers'
    hash: sha256:61b63ad03aa78e57f0017d8bda85982ec6437837fe3cdff96e12cd23ffb45b76
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An MIT-licensed plugin that gives coding agents a software development methodology as a library of composable skills — brainstorming a design, planning, subagent-driven or inline execution, test-driven development, code review and branch finishing — together with bootstrap instructions that make the agent use them."
  applicationCategory: "Coding agent skills plugin"
  featureList: "Skills library covering testing, debugging, collaboration and skill authoring; automatic skill triggering via a session-start bootstrap; subagent-driven development with two-stage review; a session-diagnosis skill; plugins for many coding agent harnesses; optional, disableable visual-companion telemetry"
  author: "Prime Radiant"
---

Superpowers describes itself as a complete software development methodology for coding agents,
built on a set of composable [[DefinedTerm/agent-skills]] and some initial instructions that make
sure the agent uses them. It is built by its creator and others at Prime Radiant, which also offers commercial support for
enterprise use, and is published on GitHub under the MIT License.

Its README describes the experience from the user's side. When the agent sees that the user is
building something, it does not start writing code; it asks what the user is really trying to do,
teases a spec out of the conversation and presents it in chunks short enough to read. Once the
design is signed off, the agent writes an implementation plan meant to be clear enough for "an
enthusiastic junior engineer with poor taste, no judgement, no project context, and an aversion to
testing" to follow, emphasizing red/green test-driven development, YAGNI and DRY. When the user says
go, it runs a [[DefinedTerm/subagent-driven-development]] process in which agents work through each
task while their work is inspected and reviewed; the README says it is not uncommon for the agent to
work autonomously for a couple of hours at a time without deviating from the plan. Because the skills
trigger automatically, nothing special has to be invoked.

## Capabilities

The README sets out a basic workflow as a sequence of skills, each activating at a particular point,
and states that the agent checks for relevant skills before any task — "Mandatory workflows, not
suggestions":

1. **brainstorming** — before code is written, refines a rough idea through questions, explores
   alternatives, presents the design in sections for validation and saves a design document.
2. **using-git-worktrees** — after design approval, creates an isolated workspace on a new branch,
   runs project setup and verifies a clean test baseline (see [[DefinedTerm/git-worktrees]]).
3. **writing-plans** — breaks the approved design into bite-sized tasks of two to five minutes each,
   every one with exact file paths, complete code and verification steps.
4. **subagent-driven-development** or **executing-plans** — either dispatches a fresh subagent per
   task with a review after each (described as the most thorough), or implements every task inline
   in the current session with one fresh review of the whole branch at the end (the cheapest).
5. **test-driven-development** — enforces RED-GREEN-REFACTOR during implementation and deletes code
   written before its tests.
6. **requesting-code-review** — between tasks, reviews against the plan and reports issues by
   severity, with critical issues blocking progress.
7. **finishing-a-development-branch** — verifies tests, presents options to merge, open a pull
   request, keep or discard the branch, and cleans up the worktree.

The wider skills library adds systematic debugging (a four-phase root-cause process),
verification-before-completion, dispatching parallel agents, receiving code review, and a
writing-skills skill for authoring new skills; in the library's own description, subagent-driven
development uses a two-stage review — spec compliance first, then code quality. A
diagnosing-superpowers skill reads a session transcript when a skill fires when it should not, stays
silent when it should fire, or the agent ignores its plan, and reports what happened with line-level
evidence. The project's stated philosophy is test-first development, systematic process over
guessing, complexity reduction, and evidence over claims.

## Adoption & Ecosystem

Installation differs by harness and has to be repeated for each one used. The README gives install
routes for [[SoftwareApplication/claude-code]] (through Anthropic's official plugin marketplace or
the project's own), [[SoftwareApplication/google-antigravity]], the [[SoftwareApplication/openai-codex]] app and CLI, [[SoftwareApplication/cursor]], Devin
CLI, Factory Droid, [[SoftwareApplication/gemini-cli]], [[SoftwareApplication/github-copilot-cli]],
Grok Build CLI, Kimi Code, [[SoftwareApplication/opencode]], Pi,
Qwen Code, [[SoftwareApplication/hermes-agent]] and Muse. On most of them a bootstrap is injected at
session start; the README notes that Hermes has no post-compaction hook, so a very long session that
compacts over its first turn loses the bootstrap and skills may stop triggering.

The project generally does not accept contributions of new skills, and requires that any change to a
skill work across all supported coding agents; skill behaviour is tested with a separate evaluation
harness. The brainstorming skill's optional visual companion loads the Prime Radiant logo from the
project's website by default, and that request includes the Superpowers version in use but no
details of the project, prompt or coding agent. The README explains that skills and plugins give
their creators no feedback, so this is how the project gets a rough idea of how many people use which
version; it is optional and can be disabled with an environment variable or through Claude Code's own telemetry opt-outs.
