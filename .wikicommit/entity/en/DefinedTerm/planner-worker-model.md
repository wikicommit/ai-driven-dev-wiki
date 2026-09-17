---
title: "Planner-Worker Model"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/self-improving-agents/'
    hash: sha256:1ff6511fbd5be98c337e7c2f62a06686ab3804b338da7c037ad479f890511e51
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A pattern for scaling to many concurrent coding agents by specializing roles: Planner agents read the codebase and spawn tasks, Worker agents implement them without needing the broader picture, and a Judge agent assesses whether the overall goal has been met."
---

The Planner-Worker model is a pattern for coordinating many AI coding agents at once by giving them specialized, hierarchical roles instead of running them as an uncoordinated swarm. Planner agents act like project managers: they read the codebase, decide what needs to be done, and spawn tasks, including recursively creating sub-tasks. Worker agents then implement those tasks without needing to track the broader project picture. At the end of an iteration, a Judge agent assesses whether the overall goal has been met.

## Usage

The pattern is attributed to a Cursor engineering experiment (credited to Wilson Lin) run after an earlier, flatter approach — many agents coordinating through a shared file-lock mechanism — produced agents that got stuck waiting on each other or became overly risk-averse, since no single agent felt responsible for the harder parts of the work in a free-for-all system. The hierarchical version is reported to have scaled to hundreds of agents working together on building a web browser, producing over a million lines of code across more than 1,000 files in a week.

A separate account, drawing on Cursor's own "Scaling long-running autonomous coding" post, describes the same three-role shape as the outcome of an explicit progression rather than a single experiment: a first, flat coordination model of equal-status agents writing to shared files with locks became a bottleneck and made agents risk-averse; a second design swapped locks for optimistic concurrency control, which removed the bottleneck without fixing coordination; and the third design, described as what runs in production now, is the Planner/Worker/Judge split, with Planners able to recursively spawn sub-planners and Judges deciding when an iteration is finished and when to restart. That post is quoted as saying "a surprising amount of the system's behavior comes down to how we prompt the agents" more than the harness or the model, and as reporting that a GPT model outperformed Opus specifically for extended autonomous work because Opus tended to stop early and take shortcuts — the same task calling for a different model in a different role.

## When It Applies

It applies when scaling beyond a small number of concurrent agents on the same codebase, where naive parallelism causes coordination conflicts (two agents claiming the same task, one agent's change breaking another's work). It assumes a codebase and task set that can genuinely be decomposed into a hierarchy the planner can reason about; the source notes this scale is not yet common in everyday development and that, for most users, going deeper with one capable long-running agent is often more practical than managing a large swarm. It pairs with Cursor's background cloud agents, in which each agent runs in its own isolated working copy via [[DefinedTerm/git-worktrees]] and merges its result back via pull request (see [[SoftwareApplication/cursor]]).

## Related Terms

[[DefinedTerm/ralph-loop]], [[DefinedTerm/agent-teams]]
