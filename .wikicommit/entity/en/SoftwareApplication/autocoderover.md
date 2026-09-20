---
title: "AutoCodeRover"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, coding-agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2508.11126'
    hash: sha256:d8a0f4c103987a46e21f37fca41b5ebfa795945e9c798921c4fdfbfc18bd9346
  - type: url
    url: 'https://arxiv.org/abs/2404.05427'
    hash: sha256:910627e9213aadf76eec527df275053539dca22c6de64a629ce02ffb7d3e1a5a
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A multi-agent system that extends collaborative coding into real-world repositories, orchestrating specialized agents that autonomously navigate, edit, and validate source code across complex multi-file projects."
  applicationCategory: "Multi-agent coding system"
  featureList: "Solves GitHub issues autonomously; code search over the abstract syntax tree using classes and methods; iterative context retrieval; spectrum-based fault localization where a test suite is available; produces a program modification or patch"
---

AutoCodeRover extends multi-agent collaboration into real-world code repositories. It orchestrates
specialized agents that autonomously navigate a codebase, edit source code, and validate the
changes, across complex projects spanning multiple files.

The paper that introduces it,
[[ScholarlyArticle/autocoderover-autonomous-program-improvement]], presents it as an automated
approach for solving GitHub issues to autonomously achieve program improvement — the software
maintenance and evolution work its authors distinguish from coding itself. In that account, LLMs are
combined with sophisticated code search capabilities, ultimately leading to a program modification
or patch.

## Capabilities

The introducing paper describes an outlook it calls more software engineering oriented than other
LLM agent approaches: AutoCodeRover works on a program representation, the abstract syntax tree,
rather than viewing a software project as a mere collection of files. Its code search exploits
program structure in the form of classes and methods, which the authors say enhances the LLM's
understanding of an issue's root cause and effectively retrieves context via iterative search.
Spectrum-based fault localization sharpens that context further, on the stated condition that a test
suite is available.

The same paper reports its measured behaviour on SWE-bench-lite, described there as 300 real-life
GitHub issues: 19% efficacy in solving them, which the authors state is higher than the recently reported
efficacy of SWE-agent, at an average cost of $0.43 USD — significantly lower, in the authors'
description, than other baselines.

## Adoption & Ecosystem

A survey on AI agentic programming classifies AutoCodeRover, in its comparative taxonomy, as a
"Multi-agent System" that is proactive, multi-turn, tool-using, and adaptive.
