---
title: "Agentless"
type: "schema:DefinedTerm"
lang: en
tags: [agents, coding-agents, llm, software-engineering, program-repair]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2407.01489'
    hash: sha256:ec78fdd1fa6d6641919d4b68279ff1e8157c8bebd09ad96bd24d862821b708e7
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An approach to solving software development problems automatically that deliberately does without an autonomous agent: a fixed three-phase process of localization, repair and patch validation in which the LLM neither decides future actions nor operates complex tools."
---

Agentless is an approach to automatically solving software development problems that deliberately
omits the autonomous agent. It is introduced in
[[ScholarlyArticle/agentless-demystifying-llm-based-software-engineering-agents]], whose authors
describe it as an agentless approach and set it against the verbose and complex setup of agent-based
approaches. In place of that setup, Agentless employs what the authors call a simplistic three-phase
process — localization, repair and patch validation — and withholds two capabilities that define an
agent in this context: the LLM does not decide future actions, and it does not operate with complex
tools.

## Usage

The term names both the specific system the paper builds and the contrast it is built to draw. The
authors' stated motivation is the question of whether complex autonomous software agents are really
necessary, given that current LLMs have limited abilities while agent-based approaches are
correspondingly complex — so "agentless" is defined by subtraction from the agent-based systems it
is compared with, rather than by a mechanism of its own beyond the three phases.

## When It Applies

The paper presents Agentless as applicable to end-to-end software development problems of the kind
agent-based systems target, and reports results on that basis: on SWE-bench Lite the authors state
that Agentless achieves both the highest performance — 32.00%, 96 correct fixes — and low cost,
$0.70, compared with all existing open-source software agents. Those are measured figures from one
evaluation rather than standing properties of the approach.

What Agentless assumes is visible in what it leaves out. Because the LLM does not decide future
actions or use complex tools, the three phases must be sufficient for the problem: the relevant code
must be findable by localization, the fix expressible as a repair, and its correctness decidable by
patch validation. The authors do not claim the approach supersedes agents — they frame it as
highlighting the currently overlooked potential of a simple, interpretable technique in autonomous
software development, and state the hope that it will help reset the baseline, starting point and
horizon for autonomous software agents and inspire future work in that direction.

The evidence behind it is one paper's own evaluation on one benchmark, together with that paper's
finding that the benchmark itself contains problems with exact ground truth patches or insufficient
and misleading issue descriptions — which is why the same authors construct
[[Dataset/swe-bench-lite-s]] as a filtered basis for more rigorous comparison.

## Related Terms

- [[Dataset/swe-bench-lite-s]] — the filtered benchmark the same paper constructs for more rigorous comparison
