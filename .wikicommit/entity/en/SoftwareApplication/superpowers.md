---
title: "Superpowers"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-skills, workflow, tdd, agentic-coding]
sources:
  - type: url
    url: 'https://nyosegawa.com/en/posts/coding-agent-workflow-2026/'
    hash: sha256:bb7d36388cc5d0dc91fc90185585f6fff68833b1b198e732c6e2d6d41a285f45
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A skill framework and development methodology that encodes spec-driven development and TDD into a single seven-stage pipeline and enforces it on the agent, adopted into the Claude Code plugin marketplace."
  applicationCategory: "DeveloperApplication"
  author: ""
  operatingSystem: ""
  softwareVersion: ""
  license: ""
---

Superpowers is a skill framework and development methodology distributed as `obra/superpowers`, described in [[BlogPosting/survey-of-development-workflows-in-the-coding-agent-era]] as having been officially adopted into the [[SoftwareApplication/claude-code]] plugin marketplace. Its distinguishing feature, in that account, is that it encodes individual practices such as [[DefinedTerm/spec-driven-development]] and TDD into a single pipeline and forces the methodology onto the agent rather than offering it as guidance.

## Overview

The survey presents it as one of four representative project workflows, and characterises its role as a guardrail that stops an agent from diving into code without thinking. Its stated fit is teams or individuals wanting full-cycle automation that layers TDD, code review and branch management on top of an SDD-style flow. In the four-way comparison it is the workflow whose focus is "forced methodology," whose verification is TDD plus code review, and whose tool dependency is high because a plugin is required.

## Features

The pipeline has seven stages. **Brainstorming** pulls requirements interactively and does not move to code until the user approves. **Git worktrees** are created automatically as isolated development branches, with the test baseline checked. **Planning** breaks approved designs into microtasks of two to five minutes each, specifying exact file paths, code specifications and validation criteria. **Execution** dispatches a new [[DefinedTerm/subagents|subagent]] per task with a two-stage review. **TDD** enforces a strict red-green-refactor cycle. **Code review** categorises the work against the plan by severity. **Branch completion** validates the test suite and presents a merge or pull request.

## History

At the time of the survey the repository is recorded at 82,074 stars in its workflow section and 82,111 in its skills-ecosystem section, where it is listed among the largest [[DefinedTerm/agent-skills]] collections.
