---
title: "Compact Filtering"
type: "schema:DefinedTerm"
lang: en
tags: [reinforcement-learning, coding-agents, training]
sources:
  - type: url
    url: 'https://www.together.ai/blog/deepswe'
    hash: sha256:607b29ec1a7476539260e91be9f97e5f5af2d90dea329b16e167e07f9a9f32f0
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A reinforcement-learning training technique for multi-turn LLM agents that masks out of the loss any trajectory that ends by reaching the maximum context length, the maximum number of environment steps, or a timeout, rather than by the agent deliberately submitting."
---

Compact filtering is a training technique for reinforcement learning (RL) on multi-turn LLM agents in
which trajectories that terminate by hitting the maximum context length, the maximum number of
environment steps, or a timeout are masked out of the loss, so that only trajectories the agent ended
deliberately contribute to training. It was introduced in
[[BlogPosting/deepswe-training-a-fully-open-sourced-state-of-the-art-coding-agent-by-scaling-rl]] as an
extension of DAPO's overlong filtering, which masks only trajectories that reach the maximum context
length; the authors' reasoning is that in multi-turn agentic settings a trajectory can also end by
timing out — through long generation or long environment execution — or by running out of steps.

## Usage

It is one component of GRPO++, the RL algorithm used to train the DeepSWE-Preview coding agent, where the
generation timeout was 20 minutes. The authors give two reasons it helps. First, it prevents or delays
reward collapse: an agent can stumble on a patch that passes all tests without knowing it, and rewarding
such runs reinforces undesired behaviour across steps — for example, answering correctly early and then
patching random files — which accumulates until training collapses; assigning reward only when the agent
deliberately submits encourages rigorous testing before the final submission. Second, it reduces
excessive thinking within each step and encourages longer reasoning across steps: in a run with compact
filtering enabled, average response length fell while the average number of environment steps rose.

## When It Applies

It applies to RL training of agents that act over many turns in an environment and whose trajectories
can end by exhaustion (context, steps, time) as well as by an explicit submit or finish action; it
assumes such a finish action exists so that deliberate termination can be told apart. The evidence for
it is a single team's report: an ablation on Qwen3-14B with and without compact filtering, and training
curves from the DeepSWE run, as presented by the authors themselves.

## Related Terms

[[DefinedTerm/trajectory-evaluation]], [[DefinedTerm/ai-coding-agent]]
