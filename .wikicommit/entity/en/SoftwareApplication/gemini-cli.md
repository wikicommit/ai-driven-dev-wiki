---
title: "Gemini CLI"
type: "schema:SoftwareApplication"
lang: en
tags: [agentic-coding, cli, ai-assisted-programming]
sources:
  - type: url
    url: 'https://arxiv.org/html/2602.14690v1'
    hash: sha256:a95102e253d7131ba8bf5f38f7f1e738784be17159af65fa612395d8ed4800b9
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The command-line agentic interface to Gemini, released in June 2025 following a Gemini Agent Mode in May 2025. It is configured through a GEMINI.md context file and a .gemini/ directory; a February 2026 study of 2,926 GitHub repositories found it the least frequently present of the five tools it examined."
  applicationCategory: "Agentic AI coding tool (CLI)"
---

Gemini CLI is the command-line agentic interface to Gemini, one of five agentic AI coding tools surveyed in [[ScholarlyArticle/configuring-agentic-ai-coding-tools]]. That study's tool timeline records Gemini's release in February 2024, a Gemini Agent Mode in May 2025, and the Gemini CLI itself in June 2025. It was the least widely present of the five in the study's sample, appearing in 186 of 2,926 repositories.

As with [[SoftwareApplication/github-copilot]] and [[SoftwareApplication/cursor]], the repository files that indicate Gemini usage apply to both its conversational and agentic interfaces, so the study cannot isolate agentic usage for it from artifact presence alone.

## Overview

Although Gemini repositories are the fewest in the sample, they are among the most active: they show the highest median contributor count of any tool group at 66, against 42 for the sample overall, and the highest median commit count at 3,322 against 2,106 overall. Their median source size, 58k KB, is also above the sample median.

## Features

Gemini exposes repository-level artifacts for six of the eight configuration mechanisms catalogued in the study:

- [[DefinedTerm/context-files]] — `GEMINI.md`
- Settings — `.gemini/settings.json` or `.gemini/config.yaml`
- [[DefinedTerm/agent-skills]] — `.gemini/skills/`
- Commands — `.gemini/commands/`
- Hooks — defined within `.gemini/settings.json`
- MCP servers — also configured via `.gemini/settings.json`

It offers neither [[DefinedTerm/subagents]] nor Rules.

## History

The study's timeline places Gemini's initial release in February 2024, its agent mode in May 2025, and the CLI in June 2025. Its context file, `GEMINI.md`, remains rare in practice: the study found 159 of them, 3.3% of all context files in the sample. GEMINI.md was also among the context file types observed acting as a pointer to other files, with the study noting it behind CLAUDE.md and AGENTS.md in outgoing references.
