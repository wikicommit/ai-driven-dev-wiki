---
title: "Harness Engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agent-architecture, evaluation, agent-tooling]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agent-harness-engineering/'
    hash: sha256:7fc8b9bc3a19589c08e3c6ab46607839f3c435799f128886bea9bca6cd634760
  - type: url
    url: 'https://developers.googleblog.com/the-anatomy-of-harness-engineering-how-to-evaluate-iterate-and-guard-ai-coding-agents/'
    hash: sha256:b7703e83eb963ad1264b1927a931ffc37279d57efe136cc6d02e664b3df6aa63
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "The discipline of treating the scaffolding built around an AI model — prompts, tools, context policies, hooks, sandboxes, feedback loops — as a real engineering artifact, rather than treating model choice as the main lever on agent behavior."
---

Harness engineering is the discipline of designing and maintaining the "harness" around an AI model — the prompts, tools, context policies, hooks, sandboxes, subagents, feedback loops, and recovery paths that turn a raw model into a working agent. It is summarized, in a formulation Addy Osmani's post attributes to Viv Trivedy, as "agent = model + harness": the model is one input, and the harness is everything else that gives it state, tool execution, feedback loops, and enforceable constraints.

## Usage

The term is applied to coding agents such as Claude Code, Cursor, Codex, Aider, and Cline. Addy Osmani's post argues that the behaviour a user experiences from these agents is dominated by what the harness does even where the model underneath is the same, and observes that set side by side they look more like each other than their underlying models do — the models differ while the harness patterns converge. The practice covers concrete components including the filesystem and Git for durable state, bash and code execution as the general-purpose action mechanism, sandboxes for safe execution, memory files (e.g. `AGENTS.md`) for continual learning across sessions, techniques for mitigating context rot (compaction, tool-call offloading, progressive disclosure of skills), long-horizon execution patterns (the Ralph Loop, planning, planner/evaluator splits), and hooks that enforce rules deterministically rather than relying on a model to remember them.

## Evaluating a Harness

A Google engineering team writing on the same discipline argues that how a harness is evaluated is
part of engineering it. They treat end-to-end benchmarks as the de facto way to evaluate model
performance and to decide what needs deeper investigation, but argue they are a poor instrument for
iteration: on their account, running suites such as Terminal-Bench and DeepSWE moves a composite
score by a few percentage points without typically saying directly why it changed. Their proposed complement is
[[DefinedTerm/behavioral-evaluation]] — fast, deterministic, unit-style assertions on discrete
observable actions the agent takes, such as which tool it called or which file it modified — which
they describe as integration tests for harness operation and as an iteration partner that shows
whether a prompt tweak, tool schema change or model upgrade made the agent holistically worse.

They also place evaluation in time: a team bootstrapping an agent starts with developer instinct
and dogfooding, and until the agent can dogfood its own codebase they argue it does not make sense
to run evaluations at all. Their closing position is that the two kinds are complementary rather
than substitutes, with macro benchmarks verifying the final destination and micro behavioural evals
enabling safe, rapid iteration. This is one team's recommended practice published on their
employer's developer blog, not a measured comparison.

## When It Applies

The practice treats an agent's mistakes as permanent signals rather than isolated incidents: a specific observed failure is encoded as a rule, a hook, or a check, and a rule is only removed once a more capable model has made it redundant — so a harness is described as shaped by its own failure history rather than something that can be downloaded ready-made. It applies where an agent is expected to work with some autonomy over multiple steps. Osmani's post also describes a way of over-applying the mindset, in a point it credits to Anthropic's own write-up: treating harness components as permanent rather than revisiting them as models improve, since a component that once compensated for a model limitation can become dead weight once that limitation is gone.

The term and its "agent = model + harness" formulation are attributed by Osmani's post to Viv Trivedy, whose own write-up it credits as the clearest derivation of what a harness is and why each piece exists; that post also draws on Dex Horthy, HumanLayer, Anthropic's own engineering team and Birgitta Böckeler, describing itself as an attempt to pull those threads together.

## Related Terms

[[DefinedTerm/ralph-loop]], [[DefinedTerm/harness-as-a-service]], [[DefinedTerm/context-rot]], [[DefinedTerm/compaction]], [[DefinedTerm/agents-md]], [[DefinedTerm/behavioral-evaluation]]
