---
title: "Cursor"
type: "schema:SoftwareApplication"
lang: en
tags: [agentic-coding, ide, ai-assisted-programming]
sources:
  - type: url
    url: 'https://arxiv.org/html/2602.14690v1'
    hash: sha256:a95102e253d7131ba8bf5f38f7f1e738784be17159af65fa612395d8ed4800b9
  - type: url
    url: 'https://en.wikipedia.org/wiki/Cursor_(company)'
    hash: sha256:2740283a56e7587ebb2885c77ada0407709764d7ed9cc1fe197276bd2f7e6fc7
  - type: url
    url: 'https://cursor.com/blog/semsearch'
    hash: sha256:157e4d6a1147f217b21dc17ae116534a1fa413895b2162f592cc28adf71e1915
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An AI coding tool first released in March 2023 that later gained agentic capabilities, with Cursor Agents added in June 2025 and a CLI in August 2025. A February 2026 study of 2,926 GitHub repositories found that repositories using it emphasise the Rules and Commands mechanisms more than those using the other tools examined."
  applicationCategory: "AI coding tool with agentic capabilities"
  author: "[[Organization/anysphere]]"
---

Cursor is an AI coding tool that gained agentic capabilities after its initial release. [[ScholarlyArticle/configuring-agentic-ai-coding-tools]] records its release in March 2023, Cursor Agents in June 2025, and a Cursor CLI in August 2025. It appeared in 355 of the 2,926 repositories in that study's sample, the second least common of the five tools examined.

Cursor is distinctive in that study for its user community's configuration habits rather than its raw adoption: Cursor projects emphasise Rules and Commands where other tools' users stay closer to context files, and the Rules mechanism is concentrated almost entirely in Cursor repositories — the authors attribute this to Cursor having been one of the first tools to introduce Rules.

## Overview

Repositories adopting Cursor stand out on two metadata dimensions in the study: they are the youngest in the sample, with a median age of 5.5 years against 6.7 years overall, and the largest by source code size, with a median of 75k KB against 40k KB overall. They also have a somewhat higher median contributor count (54) and commit count (2,780) than the sample as a whole.

### Retrieval: semantic search alongside grep

[[Organization/anysphere]]'s own research writing treats codebase retrieval as one of the levers on agent quality. [[BlogPosting/improving-agent-with-semantic-search]] reports that Cursor's agent uses [[DefinedTerm/semantic-search]] — retrieving code segments that match a natural-language query — in addition to regex-based search from a tool like grep, backed by an embedding model the company trained itself and its own indexing pipelines. Its claimed effects, measured on its own [[Dataset/cursor-context-bench]] and on its own user traffic, are 12.5% higher accuracy in answering questions on average and modest gains in code retention, largest on codebases of 1,000 files or more. Its stated conclusion is that the agent "makes heavy use of grep as well as semantic search, and the combination of these two leads to the best outcomes".

## Features

Table 1 of the study lists a Cursor artifact for each of the mechanisms it catalogues:

- [[DefinedTerm/context-files]] — [[DefinedTerm/agents-md]], plus the deprecated `.cursorrules`
- Settings — `.cursor/cli.json`
- [[DefinedTerm/agent-skills]] — `.cursor/skills/`
- [[DefinedTerm/subagents]] — `.cursor/agents/`
- Commands — `.cursor/commands/`
- Hooks — `.cursor/hooks.json`
- Rules — `.cursor/rules/`
- MCP servers — `.cursor/mcp.json`

Cursor Rules, stored in `.cursor/rules/`, are a distinct mechanism from the deprecated `.cursorrules` context file and should not be confused with it.

## History

Cursor was released in March 2023, with agentic capabilities following in 2025.

Wikipedia's account of the vendor adds a product timeline alongside the study's. It describes Cursor's agent features as searching across a codebase, editing files, running terminal commands and carrying out multi-step programming tasks from natural-language instructions; records Cursor 2.0 in October 2025 as adding support for running multiple agents in parallel using git worktrees or remote machines; and notes further agents released for web, mobile, command-line and cloud environments. Bugbot, a code-review tool integrated with GitHub pull requests, launched in July 2025, and team and enterprise plans offer administrative controls, usage analytics, single sign-on, model controls and compliance features. On models, Cursor integrates third-party large language models including models from Anthropic and OpenAI alongside its own coding models. A July 2025 change to the $20 Pro plan, replacing 500 requests with a usage-metered cap, drew complaints about unexpected charges, after which the company rolled back the limits and promised refunds. That Wikipedia article carries a July 2026 maintenance banner warning it may incorporate large-language-model text and therefore unverified claims, so these product details should be treated as unconfirmed pending a primary source — see [[Organization/anysphere]]. Its `.cursorrules` context file was among the earliest such artifacts to appear, beginning in 2024, but the study found only 73 of them in the sample (1.5% of context files) — Cursor has since deprecated the file and now suggests using AGENTS.md instead. Together with [[SoftwareApplication/codex-cli]], Cursor is cited in the study as already providing native AGENTS.md support, which the authors suggest may become a baseline expectation for tool vendors.
