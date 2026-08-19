---
title: "GitHub Copilot"
type: "schema:SoftwareApplication"
lang: en
tags: [agentic-coding, ai-assisted-programming]
sources:
  - type: url
    url: 'https://arxiv.org/html/2602.14690v1'
    hash: sha256:a95102e253d7131ba8bf5f38f7f1e738784be17159af65fa612395d8ed4800b9
  - type: url
    url: 'https://docs.github.com/en/copilot/concepts/agents/about-github-agentic-workflows'
    hash: sha256:49ae0743978d367e3e6eb74444e5c4a76951e09d3460bb9315bc2e76dd795e2d
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An AI coding assistant first released in October 2021 that later gained agentic capabilities, with an agent mode added in February 2025 and a CLI in September 2025. It is configured chiefly through context files under .github/; a February 2026 study of 2,926 GitHub repositories found it the second most frequently present of the five tools it examined."
  applicationCategory: "AI coding assistant with agentic capabilities"
---

GitHub Copilot is an AI coding assistant that began as a conversational tool and later gained agentic capabilities. [[ScholarlyArticle/configuring-agentic-ai-coding-tools]] records its original release in October 2021, an agent mode added in February 2025, and a Copilot CLI in September 2025. In that study's sample it was the second most widely present of the five tools examined, appearing in 958 of 2,926 repositories.

The study places Copilot in a group of tools — with [[SoftwareApplication/cursor]] and [[SoftwareApplication/gemini-cli]] — whose conversational and agentic modes share the same repository files, meaning artifact-based detection cannot separate agentic from conversational usage for them.

## Overview

Copilot repositories rarely extend beyond [[DefinedTerm/context-files]]; the study groups them with [[SoftwareApplication/codex-cli]] in this respect, in contrast to Claude Code's broad configuration footprint and Cursor's emphasis on Rules and Commands. Repositories adopting Copilot were the oldest in the sample, with a median age of 7.1 years.

## Features

Copilot supports four of the eight configuration mechanisms catalogued in the study through repository-level files:

- [[DefinedTerm/context-files]] — `.github/copilot-instructions.md` and `.github/instructions/*.md`. Copilot also reads the other tools' context file formats: CLAUDE.md, [[DefinedTerm/agents-md]], and GEMINI.md
- [[DefinedTerm/agent-skills]] — `.github/skills/`
- [[DefinedTerm/subagents]] — `.github/agents/`
- Hooks — `.github/hooks/*.json`

Settings and MCP servers are configured through the GitHub web interface rather than through files in the project repository, so they fall outside the study's file-based detection. Copilot offers neither Commands nor Rules.

### As the default engine for agentic workflows

GitHub's documentation for [[SoftwareApplication/github-agentic-workflows]] names Copilot as the default coding agent for those workflows: multiple engines are supported and selected through a frontmatter `engine` property — the others named being Anthropic Claude, OpenAI Codex and Google Gemini — and "GitHub Copilot is the default engine if none is specified." Using it requires a GitHub Copilot plan, and each engine needs its own authentication secret configured in the repository.

The billing path differs by engine and is documented in Copilot's terms for the default case: inference is metered in AI Credits (`1 AIC = $0.01 USD`), and for the default Copilot engine that AIC usage maps to AI credits in GitHub Copilot billing, where a third-party engine is billed by its own provider instead. For organization-owned repositories where the organization has a Copilot plan, GitHub recommends billing to the organization via the built-in `GITHUB_TOKEN` rather than a personal access token: an organization administrator enables "Copilot CLI" and "Allow use of Copilot CLI billed to the organization" in Copilot policy settings, and each workflow declares `copilot-requests: write` under its frontmatter `permissions`. GitHub notes that if the Actions token lacks Copilot access from the organization, the workflow fails when it sends Copilot requests and a `COPILOT_GITHUB_TOKEN` must be configured instead.

## History

Released in October 2021, Copilot predates the agentic tools in the study by several years; its agentic capabilities arrived with agent mode in February 2025 and the Copilot CLI in September 2025. Its context file, copilot-instructions.md, was among the artifacts that began appearing in 2024 and grew after agentic capabilities were introduced, reaching 1,344 files across the sample (27.7% of context files) and appearing in 35.1% of repositories. It is the dominant context file type in repositories whose main language is Java, C#, or C++ — the exception to CLAUDE.md's lead across other languages. The study also observes that repositories which began with copilot-instructions.md often later added CLAUDE.md or AGENTS.md, despite Copilot already supporting all major context file types.
