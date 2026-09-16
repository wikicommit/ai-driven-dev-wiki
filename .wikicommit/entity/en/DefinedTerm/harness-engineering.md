---
title: "Harness Engineering"
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
  description: "The discipline of treating the scaffolding built around an AI model — prompts, tools, context policies, hooks, sandboxes, feedback loops — as a real engineering artifact, rather than treating model choice as the main lever on agent behavior."
---

Harness engineering is the discipline of designing and maintaining the "harness" around an AI model — the prompts, tools, context policies, hooks, sandboxes, subagents, feedback loops, and recovery paths that turn a raw model into a working agent. It is summarized, in a formulation the source attributes to Viv Trivedy, as "agent = model + harness": the model is one input, and the harness is everything else that gives it state, tool execution, feedback loops, and enforceable constraints.

## Usage

The term is applied to coding agents such as Claude Code, Cursor, Codex, Aider, and Cline, which are described as differing more in harness design than in the underlying models they run on. The practice covers concrete components including the filesystem and Git for durable state, bash and code execution as the general-purpose action mechanism, sandboxes for safe execution, memory files (e.g. `AGENTS.md`) for continual learning across sessions, techniques for mitigating context rot (compaction, tool-call offloading, progressive disclosure of skills), long-horizon execution patterns (the Ralph Loop, planning, planner/evaluator splits), and hooks that enforce rules deterministically rather than relying on a model to remember them.

## When It Applies

The practice treats an agent's mistakes as permanent signals rather than isolated incidents: a specific observed failure is encoded as a rule, a hook, or a check, and a rule is only removed once a more capable model has made it redundant — so a harness is described as shaped by its own failure history rather than something that can be downloaded ready-made. It applies where an agent is expected to work with some autonomy over multiple steps. The source also describes a way of over-applying the mindset: treating harness components as permanent rather than revisiting them as models improve, since a component that once compensated for a model limitation can become dead weight once that limitation is gone.

The term and its "agent = model + harness" formulation are attributed in the source to Viv Trivedy, whose "Anatomy of an Agent Harness" post is credited as the clearest derivation of the concept; the source also cites Dex Horthy, HumanLayer, Anthropic's own engineering team, and Birgitta Böckeler as independently converging on related framings of the same idea.

## Related Terms

[[DefinedTerm/ralph-loop]], [[DefinedTerm/harness-as-a-service]], [[DefinedTerm/context-rot]], [[DefinedTerm/compaction]], [[DefinedTerm/agents-md]]
