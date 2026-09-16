---
title: "Ralph Loop"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agent-harness-engineering/'
    hash: sha256:7fc8b9bc3a19589c08e3c6ab46607839f3c435799f128886bea9bca6cd634760
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A harness pattern for autonomous long-horizon work in which a hook intercepts the model's attempt to exit and re-injects the original prompt into a fresh context window, so each iteration starts clean but reads state from the previous one through the filesystem."
---

The Ralph Loop is a harness pattern for turning a single-session coding agent into a multi-session one. A hook intercepts the model's attempt to exit and re-injects the original prompt into a fresh context window, forcing the agent to continue working against a completion goal. Each iteration starts with a clean context but reads the state left behind by the previous iteration through the filesystem.

## Usage

It is presented as a technique for autonomous long-horizon work, alongside planning (decomposing a goal into steps recorded in a plan file) and planner/generator/evaluator splits, as a way to work around models' tendency toward early stopping, poor decomposition of complex problems, and incoherence across long stretches of work.

## When It Applies

It applies where a task is expected to run longer than a single context window can hold and needs to continue unattended between iterations. It assumes durable state on the filesystem that each fresh context window can read to pick up where the previous one left off, and a hook mechanism able to intercept an exit attempt and re-inject the original prompt.

The source discusses it as an established pattern it has written about previously (in earlier posts on self-improving agents and on 2026 engineering trends) rather than as a new proposal, without attributing its origin to a specific person.

## Related Terms

[[DefinedTerm/harness-engineering]], [[DefinedTerm/context-rot]]
