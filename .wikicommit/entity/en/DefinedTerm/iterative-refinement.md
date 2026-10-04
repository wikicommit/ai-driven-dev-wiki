---
title: "Iterative refinement"
type: "schema:DefinedTerm"
lang: en
tags: [prompting, agentic-coding, verification]
sources:
  - type: url
    url: 'https://github.com/FlorianBruniaux/claude-code-ultimate-guide/blob/main/guide/workflows/iterative-refinement.md'
    hash: sha256:76f1517fd4fb3d45eeeac738cd655ba37364639f67c145dd11149406e32e52f4
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5"
generated_with: "0.9.0"

properties:
  description: "The working loop of prompting an AI coding agent, evaluating what it produces against stated criteria, giving specific feedback, and repeating until the result is good enough — described by the Claude Code Ultimate Guide as the core loop of AI-assisted development."
---

Iterative refinement is the loop of prompting an AI coding agent with a clear goal and constraints, evaluating the output against criteria, giving specific feedback on what to change and why, and repeating until the result is satisfactory. The workflow chapter of the Claude Code Ultimate Guide that describes it calls it "the core loop of effective AI-assisted development", summarized as "prompt, observe, reprompt until satisfied", and puts its key insight as specific feedback beating vague feedback.

## Usage

**Feedback.** The guide treats the quality of the feedback in each round as what makes the loop work. Effective feedback names a specific location, states a clear action, gives the reason for the change, and marks priority (for example, separating a critical security fix from a nice-to-have). Its examples of ineffective feedback — "make it better", "this is wrong", "I don't like it", "fix the bugs" — fail for want of direction, specifics or an objective criterion, and each has a concrete counterpart that states what should change.

**Autonomous loops.** The same loop can be run by the agent on itself, given explicit completion criteria — tests passing, no type errors, zero lint warnings, or measurable targets such as a response-time percentile, coverage or bundle size — and an iteration limit with an early stop when improvement falls below a threshold. The guide calls the self-improvement form the Ralph Wiggum pattern (see [[DefinedTerm/ralph-loop]]). In [[SoftwareApplication/claude-code]] it matches the trigger for the next round to the need: manual feedback where a person must judge the result, the `/goal` command for a bounded, verifiable task pursued across turns, and `/loop` for rechecking an external state periodically. It describes supporting the loop with the task tool to track each refinement as a task, with [[DefinedTerm/agent-hooks]] that run lint and tests after each edit so the agent sees failures and corrects itself, with `/compact` when context grows, and with checkpoints that commit progress and list what remains.

**Strategies.** The guide describes ordering rounds breadth-first (fix every issue at one level, such as all type errors, before the next), depth-first (finish one area completely before moving on) or by priority (security, then data integrity, then user experience, then style). For script and automation generation, which it singles out as where the loop pays off most, it says most production-ready scripts emerge after three to seven iterations: basic functionality first, then constraints and edge cases, then hardening with error handling, logging and input validation, then polish.

A specialized form for code review — review, fix and re-review within a fixed budget — is described separately as the [[DefinedTerm/review-auto-correction-loop]].

## When It Applies

It applies whenever an agent's first output is a draft to be steered toward a requirement, and it assumes the person (or, in the autonomous form, a check) can evaluate each output against stated criteria. The guide lists the ways it goes wrong: a moving target, where the approach is changed repeatedly instead of committing to one and restarting explicitly if it proves wrong; a perfectionism loop, with no "good enough" criteria to stop on; lost context, where the goal is forgotten after many rounds unless it is periodically restated; and, in autonomous form, an infinite loop when no iteration limit is set. For scripts it adds hallucinated commands for the wrong platform, missing input validation, over-engineering, requirements drifting out of context after several iterations, and shell-feature assumptions, countered by stating the constraint in the prompt or, for drift, by asking for a recap of the current requirements before the next change. For long-running and multi-day automation it advises saving state to files on disk rather than relying on the conversation. The guide rates the pattern "Tier 2 (validated pattern observed across many Claude Code users)"; its figure of 70–90% time savings for script generation is attributed to practitioner reports rather than a measurement.

## Related Terms

- [[DefinedTerm/review-auto-correction-loop]] — the bounded review-fix-re-review form
- [[DefinedTerm/ralph-loop]]
- [[DefinedTerm/verification-loop]]
- [[DefinedTerm/agent-hooks]]
- [[DefinedTerm/checkpoint-and-resume]]
