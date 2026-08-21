---
title: "Symphony"
type: "schema:SoftwareApplication"
lang: en
tags: [orchestration, multi-agent, issue-tracking, agentic-coding]
sources:
  - type: url
    url: 'https://nyosegawa.com/en/posts/coding-agent-workflow-2026/'
    hash: sha256:bb7d36388cc5d0dc91fc90185585f6fff68833b1b198e732c6e2d6d41a285f45
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An experimental OpenAI orchestrator built on the principle of managing the work that needs doing rather than the agents doing it: it polls a kanban board for Todo tickets, moves them through implementation in isolated workspaces, and hands them to human review."
  applicationCategory: "DeveloperApplication"
  author: "[[Organization/openai]]"
  operatingSystem: ""
  softwareVersion: ""
  license: ""
---

Symphony is an experimental orchestrator from OpenAI, labelled an engineering preview, whose organising concept — as reported in [[BlogPosting/survey-of-development-workflows-in-the-coding-agent-era]] — is to "manage the work that needs doing (issues), not the agents." It raises the abstraction level of orchestration from directing agents to managing tasks through an issue tracker.

## Overview

It polls kanban boards such as Linear continuously, detects tickets in Todo, autonomously moves them to In Progress, and on completion of validation moves them to Human Review. The survey presents it as the highest-abstraction orchestration in its tour of the field, and notes that the author's own idea-driven workflow resembles it.

## Features

Four capabilities are named: physical workspace isolation, with an independent workspace generated per task and [[SoftwareApplication/codex]] deployed into it; policy-as-code through a `WORKFLOW.md` file; OTP-based self-healing and retry, built on Elixir; and remote distributed execution across multiple SSH workers.

## History

The survey is explicit that this remains an experimental prototype. It records that Symphony operates by default without strong guardrails, and states as an absolute prerequisite for adoption that harness engineering — deterministic tests, linters, and CI-based automatic verification — is already properly in place in the codebase.
