---
title: "Git worktrees"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/coding-agents-manager/'
    hash: sha256:fc697c3fcc830075a1a6b6751a1f242d4b6ff4ea9a385c1ec60a0c6f8a6e50a1
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A Git feature that checks out multiple branches of the same repository at once, each into its own directory, used in agentic coding to give each of several parallel coding agents an isolated copy of the codebase to work in."
---

Git worktrees let a developer check out multiple branches of the same repository at once, each in its own directory, from a single repo. In agentic coding, this gives each of several parallel agents its own isolated working copy of the codebase, so their changes don't interfere with each other while they run.

## Usage

Osmani describes [[SoftwareApplication/claude-code]]'s own documentation as explicitly recommending git worktrees for parallel sessions so instances don't interfere with each other, and cites Anthropic's best-practices guidance as giving a step-by-step for using worktrees together with "one terminal tab per worktree" as an operating pattern. He pairs the technique with explicit boundary rules borrowed from team coordination: one agent owns one pull request, with no mega-PRs assembled from multiple agents; if two agents might touch the same files, the task split is redesigned instead; and shared interfaces are handled in a first, human-led pull request that agents then build on top of.

## When It Applies

Git worktrees apply when running several coding agents in parallel against the same repository, to prevent them from editing the same working copy at once. The source frames isolated directories alone as insufficient — merge conflicts are described as a boundary failure rather than a tooling failure, so worktrees are paired with the task-boundary rules above rather than used as a substitute for them. The practice is presented, per Osmani's account, as a recommended pattern in both Claude Code's own documentation and Anthropic's best-practices guidance, rather than as this post's own invention.

A later post describes [[SoftwareApplication/cursor]]'s background cloud agents using the same technique at the level of a hosted product: each long-running background agent runs in its own isolated git worktree and merges its result back into the codebase via a pull request, so a task started locally can be handed to the cloud and re-attached to later without colliding with other work.

## Related Terms

[[DefinedTerm/sandboxing]], [[SoftwareApplication/claude-code]], [[SoftwareApplication/cursor]], [[DefinedTerm/planner-worker-model]]
