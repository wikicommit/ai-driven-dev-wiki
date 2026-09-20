---
title: "Agentless: Demystifying LLM-based Software Engineering Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, coding-agents, llm, software-engineering, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2407.01489'
    hash: sha256:ec78fdd1fa6d6641919d4b68279ff1e8157c8bebd09ad96bd24d862821b708e7
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The arXiv preprint that asks whether complex autonomous software agents are really necessary, and answers it by building Agentless — a three-phase localization, repair and patch-validation process that the authors report outperforming every existing open-source software agent on SWE-bench Lite at a fraction of the cost."
  author: ["Chunqiu Steven Xia", "Yinlin Deng", "Soren Dunn", "Lingming Zhang"]
  datePublished: "2024-07-01"
  abstract: "The paper observes that researchers and practitioners have built various autonomous LLM agents able to use tools, run commands, observe environment feedback and plan future actions, and asks whether that complexity is warranted given the limited abilities of current LLMs. To answer it the authors build Agentless, which replaces the verbose and complex setup of agent-based approaches with a three-phase process of localization, repair and patch validation, without letting the LLM decide future actions or operate complex tools. On SWE-bench Lite the authors report Agentless achieving both the highest performance (32.00%, 96 correct fixes) and a low cost ($0.70) compared with all existing open-source software agents. They also manually classify the benchmark's problems, find some with exact ground truth patches or insufficient and misleading issue descriptions, and construct SWE-bench Lite-S by excluding them."
  keywords: ["Software Engineering (cs.SE)", "Artificial Intelligence (cs.AI)", "Computation and Language (cs.CL)", "Machine Learning (cs.LG)"]
  citation: "arXiv:2407.01489, DOI 10.48550/arXiv.2407.01489"
---

This arXiv preprint puts a question to the agent-based approach to software engineering and answers
it with a deliberately simpler system. Its background observation is that recent advances in large
language models have significantly advanced the automation of software development tasks — code
synthesis, program repair, test generation — and that researchers and industry practitioners have
since developed various autonomous LLM agents to perform end-to-end software development tasks,
equipped with the ability to use tools, run commands, observe feedback from the environment and plan
for future actions. Against that, the authors set the complexity of those agent-based approaches
alongside the limited abilities of current LLMs and ask directly: do we really have to employ
complex autonomous software agents?

To attempt an answer they build [[DefinedTerm/agentless]], which they describe as an agentless
approach to automatically solving software development problems. Where agent-based approaches have
a verbose and complex setup, Agentless employs a simplistic three-phase process of localization,
repair and patch validation, and does so without letting the LLM decide future actions or operate
with complex tools.

The headline result the authors report is on SWE-bench Lite, where they state that the simplistic
Agentless achieves both the highest performance — 32.00%, 96 correct fixes — and low cost, $0.70,
compared with all existing open-source software agents, a result they present as surprising. A
second contribution follows from inspecting the benchmark rather than the systems: the authors
manually classified the problems in SWE-bench Lite and found problems with exact ground truth patch
or insufficient and misleading issue descriptions, and on that basis constructed
[[Dataset/swe-bench-lite-s]] by excluding such problematic issues, in order to perform a more
rigorous evaluation and comparison.

The authors frame the work as highlighting the currently overlooked potential of a simple,
interpretable technique in autonomous software development, and state the hope that Agentless will
help reset the baseline, starting point and horizon for autonomous software agents.

The preprint is filed under Software Engineering (cs.SE), with cross-listings to Artificial
Intelligence (cs.AI), Computation and Language (cs.CL) and Machine Learning (cs.LG). It was first
submitted on 1 July 2024 and revised on 29 October 2024 as version 2, and carries the arXiv-issued
DOI 10.48550/arXiv.2407.01489.

## Key Points

- The paper's motivating question is whether complex autonomous software agents are actually necessary, given that current LLMs have limited abilities and agent-based setups are correspondingly complex.
- It introduces Agentless, an agentless approach built as a three-phase process — localization, repair, patch validation — in which the LLM neither decides future actions nor operates complex tools.
- On SWE-bench Lite the authors report Agentless achieving the highest performance among all existing open-source software agents at 32.00% (96 correct fixes), at a cost of $0.70.
- A manual classification of SWE-bench Lite's problems by the authors turned up issues whose ground truth patch was exact, and issues whose descriptions were insufficient or misleading.
- On that basis the authors construct SWE-bench Lite-S, excluding the problematic issues, and present it as the basis for a more rigorous evaluation and comparison.
- The authors state their aim as resetting the baseline, starting point and horizon for autonomous software agents rather than as ruling agents out.

## Notes

The paper's argument is comparative by construction: its claim is not that the three-phase process is
good in isolation but that it beats the agent-based systems it was measured against, on one
benchmark, at a stated cost. Both halves of the contribution qualify that comparison — the authors'
own finding that some of SWE-bench Lite's problems have exact ground truth patches or misleading
descriptions is a statement about the measuring instrument used for the headline number, which is
why the filtered SWE-bench Lite-S is offered alongside it.
