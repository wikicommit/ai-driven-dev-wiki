---
title: "Codex CLI"
type: "schema:SoftwareApplication"
lang: en
tags: [agentic-coding, cli, ai-assisted-programming]
sources:
  - type: url
    url: 'https://arxiv.org/html/2602.14690v1'
    hash: sha256:a95102e253d7131ba8bf5f38f7f1e738784be17159af65fa612395d8ed4800b9
  - type: url
    url: 'https://openai.com/index/introducing-codex/'
    hash: sha256:c899f94e6c00781777e4a0c930a154bee0271654282a1a6f195b368868a1366b
  - type: url
    url: 'https://openai.com/codex/'
    hash: sha256:d885d8a80478f4aecb76134aac46d1976013ff1a1cf8ecb1eead450eeac6d72a
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An agentic AI coding tool with a command-line interface, released by OpenAI in April 2025. It reads AGENTS.md natively, and a February 2026 study of 2,926 GitHub repositories found that repositories using it rarely extend their configuration beyond context files."
  applicationCategory: "Agentic AI coding tool (CLI)"
  author: "[[Organization/openai]]"
---

Codex CLI is an agentic AI coding tool from OpenAI with a command-line interface, released in April 2025 with its CLI and agents available from launch. [[ScholarlyArticle/configuring-agentic-ai-coding-tools]] includes it as one of five major agentic coding tools; it appeared in 558 of the 2,926 repositories in that study's sample. The authors selected it in place of ChatGPT on the grounds that Codex is an agentic tool from the same vendor using the same models.

Codex was among the first tools to implement a central agent loop steered by a foundational model, alongside [[SoftwareApplication/claude-code]], before conversational tools such as [[SoftwareApplication/github-copilot]] and [[SoftwareApplication/cursor]] added comparable capabilities in an agent mode.

## Overview

Repositories using Codex rarely extend their configuration beyond [[DefinedTerm/context-files]] — the study groups them with Copilot repositories in this respect, in contrast to Claude Code's broad configuration footprint. On repository metadata, Codex repositories had a slightly lower median commit count and source size than the sample as a whole.

## Features

Codex exposes repository-level artifacts for five of the eight configuration mechanisms catalogued in the study:

- [[DefinedTerm/context-files]] — [[DefinedTerm/agents-md]] and `AGENTS.override.md`
- Settings — `.codex/config.toml`
- [[DefinedTerm/agent-skills]] — `.codex/skills/`
- Rules — `.codex/rules/`
- MCP servers — also configured via `.codex/config.toml`

It offers neither [[DefinedTerm/subagents]], Commands, nor Hooks.

## History

OpenAI's own account, written in [[BlogPosting/introducing-codex]] on 16 May 2025, describes the CLI as having launched "last month" as "a lightweight open-source coding agent that runs in your terminal", bringing models such as o3 and o4-mini into the local workflow. The same post announced two changes to it: a smaller version of `codex-1` derived from o4-mini, optimized for low-latency code Q&A and editing while retaining instruction-following and style, released as the CLI's default model and as `codex-mini-latest` in the API with the underlying snapshot to be updated regularly; and sign-in with a ChatGPT account in place of manually generating and configuring an API token, with the API key generated automatically, alongside time-limited free API credits of $5 for Plus users and $50 for Pro users.

OpenAI later folded the CLI into a single product surface. Its Codex product page presents "the same agent everywhere you code" across Codex in ChatGPT, a Codex IDE extension and Codex CLI, connected by the user's ChatGPT account — so the CLI is now positioned as one of three ways into [[SoftwareApplication/codex]] rather than as a separate tool. The launch post had already anticipated this direction, listing the ability to assign tasks from Codex CLI as a roadmap item.

Codex CLI was released in April 2025. The study notes that AGENTS.md, the tool-agnostic context file convention it reads natively, was itself introduced by OpenAI, and cites Codex alongside Cursor as tools that already provide native AGENTS.md support — which the authors suggest may become a baseline expectation for vendors as the convention converges into a cross-tool standard.
