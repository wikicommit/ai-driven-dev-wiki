---
title: "Rolling the Dice"
type: "schema:DefinedTerm"
lang: en
tags: [vibe-coding, prompt-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.22418'
    hash: sha256:f10a74dba745c31d031399f5009f9e4afada40b2a3620baed32d7616596a8ba6
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "In Chou et al.'s qualitative study of vibe coding, reissuing a prompt with the same intent as an earlier one without adding new information — rewording it, re-pasting an identical error message, or rejecting an output without explanation."
---

In [[ScholarlyArticle/building-software-by-rolling-the-dice]], Chou et al. use "rolling the dice" for the practice of reissuing prompts with similar intent without adding new information. In their prompt analysis, a prompt counts as rolling the dice — coded as "method-redundant" — when it repeats a prior intent through simple rewording, copying an identical error message, or rejecting an output without further explanation; a prompt that introduces new details or a hypothesis does not count, even if it pursues the same goal. The image echoes the vibe coders they studied, who described debugging and feature refinement — tasks expected to be deterministic — as feeling stochastic, like "throwing a dice".

## Usage

The term belongs to the study of [[DefinedTerm/vibe-coding]], where the authors tie it to how much a coder relies on AI and how much they know about the code. In their analysis of seven live-streamed sessions, the two coders with the highest reliance on AI and less relevant technical background devoted nearly 40% of their prompts to rolling the dice, often reposting error messages without elaboration, while coders who inspected code more often or drew on relevant backgrounds typically stayed under 20%. One coder who repeated the same intents avoided method-redundancy by adding hypotheses or technical specifics each time. The authors connect this to their finding that a coder's mental model of the artifacts shapes their prompting strategies.

The practitioners in the study did not agree on the framing. One described the AI's stochastic changes as a "vision quest" and recommended resetting with version control and rolling the dice again; another rejected the analogy with image generation, where rerolling works because many outputs fit the problem, arguing that in programming one pixel off is a bug. The safeguards the authors observed for reining in stochastic changes were undo, version control, small incremental changes, automated tests and linters.

## Related Terms

- [[DefinedTerm/vibe-coding]]
