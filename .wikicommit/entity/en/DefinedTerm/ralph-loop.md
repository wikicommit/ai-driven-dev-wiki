---
title: "Ralph Loop"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agent-harness-engineering/'
    hash: sha256:7fc8b9bc3a19589c08e3c6ab46607839f3c435799f128886bea9bca6cd634760
  - type: url
    url: 'https://addyosmani.com/blog/self-improving-agents/'
    hash: sha256:1ff6511fbd5be98c337e7c2f62a06686ab3804b338da7c037ad479f890511e51
  - type: url
    url: 'https://addyosmani.com/blog/code-agent-orchestra/'
    hash: sha256:f16aa303da51395585e293ea9d466a00847210974b774f822827f13f48b30431
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A harness pattern, nicknamed the 'Ralph Wiggum technique' and popularized by Geoffrey Huntley and Ryan Carson, that breaks development into small atomic tasks and runs an agent through a repeating pick/implement/validate/commit/reset cycle, resetting context each iteration to avoid accumulating confusion."
---

The Ralph Loop, also nicknamed the "Ralph Wiggum technique," is a harness pattern popularized by Geoffrey Huntley and Ryan Carson for turning a single-session coding agent into a multi-session one. Development is broken into many small tasks, and an agent works through them in a repeating cycle: pick the next task from a to-do list, implement it, validate the change (tests, type checks), commit if checks pass, update the task's status and log any learnings, then reset the agent's context and repeat. By resetting its context every iteration, the agent avoids accumulating confusion from prior tasks, trading a single enormous prompt for repeated, bounded ones.

## Usage

Four channels of memory persist across the otherwise-stateless resets: git commit history (each iteration's changes are committed, so a later iteration can inspect the diff instead of recalling it), a plain-text progress log describing what happened each cycle, a task-state file (e.g. a JSON of tasks with pass/fail flags) tracking which work remains, and an `AGENTS.md` file that accumulates discovered patterns and gotchas as long-term semantic memory every iteration can read and add to. It is presented alongside planning (decomposing a goal into steps recorded in a plan file) and planner/generator/evaluator splits as a way to work around models' tendency toward early stopping, poor decomposition of complex problems, and incoherence across long stretches of work.

## When It Applies

It applies where a task is expected to run longer than a single context window can hold and needs to continue unattended, such as overnight, between iterations. It assumes durable state on the filesystem that each fresh context window can read to pick up where the previous one left off, small tasks with unambiguous pass/fail criteria, and safeguards to keep an unattended run from causing harm: reported safeguards include running only on feature branches, feeding failing test/build output back to the agent for auto-retry, killing and reassigning an agent stuck for 3 or more iterations on the same error, hard limits on iterations/time/tokens (including per-role budgets), and opening a pull request for human review rather than merging automatically.

Two of the sources describing this pattern credit Geoffrey Huntley and Ryan Carson with popularizing it, rather than presenting it as either author's own invention; one of those two credits a standalone `ralph` tool implementation to Carson specifically. The earliest-published of the three sources discusses the pattern as one it has written about previously, without naming an originator.

## Related Terms

[[DefinedTerm/harness-engineering]], [[DefinedTerm/context-rot]], [[DefinedTerm/beads]], [[DefinedTerm/planner-worker-model]]
