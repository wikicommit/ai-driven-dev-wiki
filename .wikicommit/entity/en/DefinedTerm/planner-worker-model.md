---
title: "Planner-Worker Model"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/self-improving-agents/'
    hash: sha256:1ff6511fbd5be98c337e7c2f62a06686ab3804b338da7c037ad479f890511e51
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A pattern for scaling to many concurrent coding agents by specializing roles: Planner agents read the codebase and spawn tasks, Worker agents implement them without needing the broader picture, and a Judge agent assesses whether the overall goal has been met."
---

The Planner-Worker model is a pattern for coordinating many AI coding agents at once by giving them specialized, hierarchical roles instead of running them as an uncoordinated swarm. Planner agents act like project managers: they read the codebase, decide what needs to be done, and spawn tasks, including recursively creating sub-tasks. Worker agents then implement those tasks without needing to track the broader project picture. At the end of an iteration, a Judge agent assesses whether the overall goal has been met.

## Usage

The pattern is attributed to a Cursor engineering experiment (credited to Wilson Lin) run after an earlier, flatter approach — many agents coordinating through a shared file-lock mechanism — produced agents that got stuck waiting on each other or became overly risk-averse, since no single agent felt responsible for the harder parts of the work in a free-for-all system. The hierarchical version is reported to have scaled to hundreds of agents working together on building a web browser, producing over a million lines of code across more than 1,000 files in a week.

## When It Applies

It applies when scaling beyond a small number of concurrent agents on the same codebase, where naive parallelism causes coordination conflicts (two agents claiming the same task, one agent's change breaking another's work). It assumes a codebase and task set that can genuinely be decomposed into a hierarchy the planner can reason about; the source notes this scale is not yet common in everyday development and that, for most users, going deeper with one capable long-running agent is often more practical than managing a large swarm.

## Related Terms

[[DefinedTerm/ralph-loop]], [[DefinedTerm/agent-teams]]
