---
title: "Critic Model"
type: "schema:DefinedTerm"
lang: en
tags: [coding-agents, verification, evaluation]
sources:
  - type: url
    url: 'https://openhands.dev/blog/20260305-learning-to-verify-ai-generated-code'
    hash: sha256:672e965c31f9cb19e39209c68cf05a7789cd6435e662e2fbef87b99f6c790dfe
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A model trained to score a coding agent's work — in OpenHands' usage, its whole trajectory of conversation, tool calls and actions — so that the score can drive decisions such as continuing, stopping, refining, or choosing among several attempts."
---

A critic model is a model trained to judge a coding agent's attempt rather than to produce one. In the
form [[SoftwareApplication/openhands]] describes in [[BlogPosting/learning-to-verify-ai-generated-code]],
it is a small, fast model that scores an agent's **trajectory** — the conversation, tool calls and
actions of an attempt — and that score is then used to decide whether to continue, stop or refine, to
pick among multiple attempts, and to collect lightweight feedback that improves the agent over time.
OpenHands presents its critic as a trajectory-level verifier and the first layer of what it calls a
verification stack.

## Usage

OpenHands' post notes that earlier academic work had already trained critic models on benchmark datasets
such as SWE-bench and SWE-Gym, where verified rewards such as unit tests make it convenient to label each
attempt as correct or not. Its own argument is that such rewards usually do not exist in real-world,
human-in-the-loop development, where goals evolve and success signals are sparse or delayed, and it
reports that critics trained only on benchmark traces translated poorly to production outcomes. OpenHands
instead trains its critic on real-world user–agent interactions: each interaction is split into segments,
every segment is annotated with rubric features observable in the trace, and a small subset is grounded
in sparse outcome proxies such as whether a pull request was merged and whether the code survived. By
OpenHands' own evaluation, code survival made the stronger training signal of the two.

The post describes two ways it uses the score at inference time: **best-of-N selection**, reranking
several attempts and keeping the best, and **early stopping**, accepting an attempt as soon as its score
clears a threshold. Because the model is small, OpenHands says it is fast and cheap enough to run during
an interactive session.

## Related Terms

[[DefinedTerm/trajectory-evaluation]], [[DefinedTerm/llm-as-a-judge]], [[DefinedTerm/agent-as-a-judge]]
