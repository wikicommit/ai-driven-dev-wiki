---
title: "OpenAI Codex"
type: "schema:SoftwareApplication"
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
  description: "OpenAI's agentic coding tool, positioned around explicit tool use: it runs commands and tests, iterates until they pass, and then proposes a pull request."
  applicationCategory: "Agentic coding tool"
  featureList: "Runs commands and tests; iterates to a passing state; proposes a pull request"
  author: "OpenAI"
---

OpenAI Codex is OpenAI's agentic coding tool. Osmani describes its positioning as explicit about tool use: it runs commands, runs tests, iterates to a passing state, and then proposes a pull request.

## Capabilities

- Runs commands and tests as part of its own workflow.
- Iterates until those checks pass before proposing a pull request.
- Its documentation recommends using an [[DefinedTerm/agents-md]] file to give the agent consistent expectations about which tests to run, lint rules, dependency policies, and documentation requirements.

## Adoption & Ecosystem

The source groups Codex with other cloud agents — GitHub Copilot Agent, Claude Web, and Jules — as tools explicitly positioned for parallelizable, sandboxed tasks that can write code, run commands, and propose changes for review.
