---
title: "GitHub Copilot coding agent"
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
  description: "GitHub's asynchronous background coding agent, which works on a task in the background, opens a draft pull request, and iterates as a human comments on it."
  applicationCategory: "Agentic coding tool"
  featureList: "Opens a draft pull request; works in the background; requests review and iterates on comments"
  author: "GitHub"
---

GitHub Copilot coding agent is GitHub's asynchronous background coding agent. Osmani describes it as framing itself as a background agent that opens a draft pull request, works in the background, and then requests review, where a human can comment and have it iterate.

## Capabilities

- Works on a task asynchronously in the background rather than requiring a developer to pair with it in real time.
- Opens a draft pull request as its unit of output.
- Requests review and iterates on a human's comments.

## Adoption & Ecosystem

The source groups it with other cloud agents — Claude Web, Codex, and Jules — as tools explicitly positioned for parallelizable, sandboxed tasks that write code, run commands, and propose changes for review. It also reports that GitHub previewed "Agent HQ," a control plane for coordinating multiple third-party coding agents in one place, including running them in parallel on the same tasks to compare outputs, as part of a broader move toward "mission control" dashboards for managing multiple agents rather than one.
