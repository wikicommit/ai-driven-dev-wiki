---
title: "Ralph Loop"
type: "schema:DefinedTerm"
lang: en
tags: [harness-engineering, long-running-agents]
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
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
  - type: url
    url: 'https://blog.langchain.com/improving-deep-agents-with-harness-engineering/'
    hash: sha256:7628e7920b4c219963d45c07cb27a6039a14ef5a60f3939b0ccb424dd7481ddd
  - type: url
    url: 'https://blog.langchain.com/the-anatomy-of-an-agent-harness/'
    hash: sha256:71cffd4adc7b81b7dd5f981d26af2bebcee592b2751a882ea95bb833fa2d022e
  - type: url
    url: 'https://ghuntley.com/ralph/'
    hash: sha256:9836ee3ee0773613f370a27796b1e456199be38681f73a47b974e210dd356317
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A harness pattern, nicknamed the 'Ralph Wiggum technique' and popularized by Geoffrey Huntley and Ryan Carson, that breaks development into small atomic tasks and runs an agent through a repeating pick/implement/validate/commit/reset cycle, resetting context each iteration to avoid accumulating confusion."
---

The Ralph Loop, also nicknamed the "Ralph Wiggum technique," is a harness pattern popularized by Geoffrey Huntley and Ryan Carson for turning a single-session coding agent into a multi-session one. Development is broken into many small tasks, and an agent works through them in a repeating cycle: pick the next task from a to-do list, implement it, validate the change (tests, type checks), commit if checks pass, update the task's status and log any learnings, then reset the agent's context and repeat. By resetting its context every iteration, the agent avoids accumulating confusion from prior tasks, trading a single enormous prompt for repeated, bounded ones.

## Usage

Huntley's own post on the technique, [[BlogPosting/ralph-wiggum-as-a-software-engineer]] (July 14,
2025), gives its simplest form: Ralph is a technique, and in its purest form a Bash loop that
repeatedly pipes the same prompt file into a coding agent — `while :; do cat PROMPT.md | claude-code ;
done` — which he says can be done with any tool that does not cap tool calls and usage. The loop he
describes is a single process working autonomously in one repository and doing one thing per
iteration, with the agent trusted to pick the most important item from a plan file (`fix_plan.md`).
Each iteration loads the same plan and specifications into context; the primary context window acts
as a scheduler that hands expensive work to subagents, with only one subagent allowed to run build and
test; tests, type checkers and static analysers serve as [[DefinedTerm/backpressure]] against invalid
code; and the agent is allowed to record what it learns about building the project in an `AGENT.md`
file and to commit, push and tag once tests pass. Whenever the agent misbehaves, the operator "tunes"
it by adding an instruction to the prompt — the post's recurring image is putting up a sign for Ralph —
and a separate planning prompt regenerates the to-do list when it runs out or goes off track.

In the form Addy Osmani's posts describe, four channels of memory persist across the otherwise-stateless resets: git commit history (each iteration's changes are committed, so a later iteration can inspect the diff instead of recalling it), a plain-text progress log describing what happened each cycle, a task-state file (e.g. a JSON of tasks with pass/fail flags) tracking which work remains, and an `AGENTS.md` file that accumulates discovered patterns and gotchas as long-term semantic memory every iteration can read and add to. It is presented alongside planning (decomposing a goal into steps recorded in a plan file) and planner/generator/evaluator splits as a way to work around models' tendency toward early stopping, poor decomposition of complex problems, and incoherence across long stretches of work.

## When It Applies

It applies where a task is expected to run longer than a single context window can hold and needs to continue unattended, such as overnight. It assumes durable state on the filesystem that each fresh context window can read to pick up where the previous one left off, small tasks with unambiguous pass/fail criteria, and safeguards to keep an unattended run from causing harm: reported safeguards include running only on feature branches, feeding failing test/build output back to the agent for auto-retry, killing and reassigning an agent stuck for 3 or more iterations on the same error, hard limits on iterations/time/tokens (including per-role budgets), and opening a pull request for human review rather than merging automatically.

Three of the Addy Osmani posts describing this pattern credit Geoffrey Huntley and Ryan Carson with popularizing it, rather than presenting it as either author's own invention, and one of them credits a standalone `ralph` tool implementation to Carson specifically. The fourth, "Agent Harness Engineering" (April 19, 2026), discusses the pattern as one its author has written about before, without naming an originator, and describes it there as a hook that intercepts the model's attempt to exit and re-injects the original prompt into a fresh context.

Two LangChain posts describe the hook-based form from the harness-design side. [[BlogPosting/the-anatomy-of-an-agent-harness]] defines the Ralph Loop as a harness pattern that intercepts the model's attempt to exit through a hook and reinjects the original prompt into a clean context window, forcing the agent to continue its work against a completion goal; it adds that the filesystem is what makes this possible, since each iteration starts with fresh context but reads the state the previous one left. [[BlogPosting/improving-deep-agents-with-harness-engineering]] calls it a "Ralph Wiggum Loop" — a hook that forces the agent to continue executing on exit — and reports borrowing the mechanism for a different end: a middleware that intercepts LangChain's coding agent before it exits and reminds it to run a verification pass against the task specification.

Huntley's post sets its own limits. He presents the technique as suited to bootstrapping greenfield
projects, with the expectation of getting about 90% of the way, says he would not use it in an
existing codebase, and holds that senior engineering expertise is still needed to guide it. The
failures he reports are a model bias toward placeholder or minimal implementations, duplicate
implementations when the agent's code search wrongly concludes something is missing — which he calls
the technique's Achilles' heel — errors in the specifications themselves, and waking to a codebase
that no longer compiles, where the operator must choose between resetting and writing new prompts.
These come from his own experience building a programming language with it, not from a measured
comparison.

## Related Terms

[[DefinedTerm/harness-engineering]], [[DefinedTerm/context-rot]], [[DefinedTerm/beads]], [[DefinedTerm/planner-worker-model]], [[DefinedTerm/backpressure]]
