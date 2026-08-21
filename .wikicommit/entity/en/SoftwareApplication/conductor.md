---
title: "Conductor"
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
  description: "A macOS local orchestrator by Melty Labs that runs several Claude Code and Codex agents in parallel, each in its own git worktree, with a visual dashboard and a diff-first review interface."
  applicationCategory: "DeveloperApplication"
  author: "Melty Labs"
  operatingSystem: "macOS"
  softwareVersion: ""
  license: ""
---

Conductor is a local multi-agent orchestrator for macOS, made by Melty Labs. It runs several [[SoftwareApplication/claude-code]] and [[SoftwareApplication/codex]] agents in parallel, giving each its own git worktree, and presents them through a visual dashboard with a diff-first review interface.

## Overview

In the three-tier framing [[BlogPosting/the-code-agent-orchestra]] uses for the 2026 tool landscape, Conductor sits in Tier 2 — local orchestrators, where the developer's own machine spawns agents in isolated worktrees and the developer stays in the loop through dashboards, diff review, and merge control. Osmani describes it as the fastest way to start multi-agent orchestration on a Mac and names its sweet spot as three to eight parallel features on the same repository with visual oversight.

## Features

Parallel execution of multiple Claude Code and Codex agents, one git worktree per agent, a visual dashboard of running work, and a review interface built around diffs. The worktree lifecycle work that would otherwise be done with a handful of shell aliases — create worktree and branch, start agent, rebase and open a PR, clean up finished worktrees — is handled visually.

## History

The account available here states that it is free, with the user paying only their own API costs, and that it is macOS-only for now, supporting both Apple Silicon and Intel machines.
