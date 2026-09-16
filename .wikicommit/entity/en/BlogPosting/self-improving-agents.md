---
title: "Self-Improving Coding Agents"
type: "schema:BlogPosting"
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
  description: "A practical guide to setting up autonomous, overnight coding-agent loops: orchestrating the loop, structuring AGENTS.md and other memory files, validating output with tests, scaling to concurrent agents, and managing the risks of unattended autonomous execution."
  author: "Addy Osmani"
  datePublished: "2026-01-31"
---

This post is a practical guide to setting up autonomous coding-agent loops that keep working while a developer is away, expanding on techniques Ryan Carson described for making an agent "learn and ship while you sleep." It covers orchestrating the loop itself, structuring persistent memory across iterations, validating output with automated tests, scaling to multiple concurrent agents, and managing the risks of running agents with commit access and shell execution rights unattended.

Its central pattern is the [[DefinedTerm/ralph-loop]] (nicknamed the "Ralph Wiggum technique," popularized by Geoffrey Huntley and Ryan Carson): breaking development into small, atomic tasks and running an agent through a repeating pick-implement-validate-commit-reset cycle, resetting the agent's context each time to avoid accumulating confusion.

## Key Points

- It sets out the loop's six-step cycle: pick the next task from a to-do list, implement it, validate with tests/type checks, commit if checks pass, update task status and log learnings, then reset the agent's context and repeat.
- It describes four channels of memory that persist across an otherwise stateless loop: git commit history, a plain-text progress log, a task-state file (e.g. a JSON of tasks with pass/fail flags), and an AGENTS.md file acting as long-term semantic memory that every iteration reads and can append to.
- It recommends structuring AGENTS.md into sections — Patterns & Conventions, Gotchas, Style/Preferences, Recent Learnings — kept brief and factual, and warns that as the file grows, injecting all of it into every prompt risks context bloat that degrades performance.
- Citing Simon Willison, it reports that the most effective way to get an agent to write good tests is to maintain high-quality tests already in the codebase for the agent to imitate.
- Citing a Cursor engineering experiment, it describes a "[[DefinedTerm/planner-worker-model]]" in which specialized Planner agents decompose work and Worker agents implement it, reporting this scaled to hundreds of agents building a web browser and producing over a million lines of code across 1,000+ files in a week, after an earlier shared-file-locking approach caused agents to get stuck or become overly risk-averse.
- It recommends running agents only on feature branches (never main), auto-approving only read-only commands while requiring approval for writes, and sandboxing execution (e.g. in a container); separately, it recommends keeping a hard maximum-iterations limit (and time/idle limits) to bound runaway costs.
- It names hallucination and "task divergence" (misinterpreting a requirement) as the main correctness risks, and recommends mitigating them with unambiguous acceptance criteria, validation via tests/type checks, periodic fresh-start replanning to counter long-run drift, and cross-checking with a second model where available.
- It reports Compound Product (an open-source system by Ryan Carson's team) chains an Analysis loop, a Planning loop, and an Execution loop so that one agent's output becomes the next loop's input, with the philosophy that "each improvement should make future improvements easier."

## Context

The post presents itself explicitly as a complement to Ryan Carson's own write-up on the same technique, crediting him and Geoffrey Huntley with popularizing the loop pattern, and draws additional practices from Eric J. Ma's and Simon Willison's separately published writing on agent memory and testing. Claims about specific implementations (Carson's `ralph` tool, Compound Product, the Cursor Planner-Worker experiment) are attributed to those named sources rather than presented as the author's own results.
