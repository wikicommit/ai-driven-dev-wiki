---
title: "Vibe Kanban"
type: "schema:SoftwareApplication"
lang: en
tags: [multi-agent, orchestration, agentic-coding, git-worktree]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/code-agent-orchestra/'
    hash: sha256:399fcd256a0dea0d4dc0841558f7f17cf41a9b447bc6bbc5adfbaf8728e9c557
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A cross-platform kanban board for coordinating parallel coding agents: each task card gets its own git worktree and branch, with diffs reviewed in-board and feedback sent to running agents."
  applicationCategory: "DeveloperApplication"
  author: ""
  operatingSystem: "macOS, Windows, Linux"
  softwareVersion: ""
  license: ""
---

Vibe Kanban is a cross-platform local orchestrator that organises parallel coding-agent work as a kanban board. Task cards carry detailed prompts; dragging a card to "In Progress" gives that task its own git worktree and branch, and diffs are reviewed inside the board with feedback sent to agents while they are still running.

## Overview

[[BlogPosting/the-code-agent-orchestra]] places it in Tier 2 of its tool landscape — local orchestrators — and describes the specific problem it targets as the "doomscrolling gap": the two to five minutes while an agent is working and the developer has nothing to do. Making the queue of parallel work visible as a board is the answer it offers to that idle time.

## Features

Task cards with detailed prompts, a worktree and branch per task, in-board diff review, and the ability to send feedback to a running agent. It supports [[SoftwareApplication/claude-code]], [[SoftwareApplication/codex]], [[SoftwareApplication/gemini-cli]], Amp, [[SoftwareApplication/cursor]] Agent CLI, and others.

## History

The account available here states that it runs on Mac, Windows and Linux, is free, and is bring-your-own-key.
