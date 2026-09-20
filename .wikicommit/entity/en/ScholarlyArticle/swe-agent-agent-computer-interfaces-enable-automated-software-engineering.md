---
title: "SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, coding-agents, llm, software-engineering, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2405.15793'
    hash: sha256:ebb2c6da508182de8f896253125e9ab51d33562a0f61627a99fbb416053c71ec
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The arXiv preprint that introduces SWE-agent, a system letting language model agents autonomously use computers to solve software engineering tasks, and argues that the design of its custom agent-computer interface is what drives the agent's performance."
  author: ["John Yang", "Carlos E. Jimenez", "Alexander Wettig", "Kilian Lieret", "Shunyu Yao", "Karthik Narasimhan", "Ofir Press"]
  datePublished: "2024-05-06"
  abstract: "The paper posits that language model agents are a new category of end users with their own needs and abilities, and that — like humans working with integrated development environments — they would benefit from interfaces built specifically for them. It investigates how interface design affects the performance of language model agents and, out of that exploration, introduces SWE-agent, a system that facilitates LM agents in autonomously using computers to solve software engineering tasks. The authors report state-of-the-art results on SWE-bench and HumanEvalFix, with pass@1 rates of 12.5% and 87.7% respectively, and close with observations on how the design of the agent-computer interface shapes agent behavior and performance."
  keywords: ["Software Engineering (cs.SE)", "Artificial Intelligence (cs.AI)", "Computation and Language (cs.CL)", "Human-Computer Interaction (cs.HC)", "Machine Learning (cs.LG)"]
  citation: "arXiv:2405.15793, DOI 10.48550/arXiv.2405.15793"
---

This arXiv preprint introduces [[SoftwareApplication/swe-agent]] and makes an argument about why it
works. Its starting observation is that language model agents are increasingly used to automate
complicated tasks in digital environments, and its proposal is to treat those agents as a new
category of end users — ones with their own needs and abilities, who would benefit from
specially-built interfaces to the software they use, just as humans benefit from powerful
applications such as integrated development environments when doing complex work like software
engineering.

From that premise the paper investigates how interface design affects the performance of language
model agents, and introduces SWE-agent as the result of that investigation: a system that
facilitates LM agents in autonomously using computers to solve software engineering tasks. The
component the paper singles out is SWE-agent's custom [[DefinedTerm/agent-computer-interface]]
(ACI), which the authors state significantly enhances an agent's ability to create and edit code
files, navigate entire repositories, and execute tests and other programs.

The authors evaluate SWE-agent on [[Dataset/swe-bench]] and on HumanEvalFix, reporting
state-of-the-art performance on both with pass@1 rates of 12.5% and 87.7% respectively — figures
they describe as far exceeding the previous state of the art achieved with non-interactive language
models. The paper closes by offering insight into how the design of the ACI can affect agents'
behavior and performance.

The preprint is filed under Software Engineering (cs.SE), with cross-listings to Artificial
Intelligence (cs.AI), Computation and Language (cs.CL), Human-Computer Interaction (cs.HC) and
Machine Learning (cs.LG). It was first submitted on 6 May 2024 and last revised on 11 November 2024
as version 3, and carries the arXiv-issued DOI 10.48550/arXiv.2405.15793. Code, data and a demo are
stated to be available at <https://swe-agent.com>.

## Key Points

- The paper's framing claim is that LM agents represent a new category of end users with their own needs and abilities, and therefore would benefit from interfaces built specifically for them rather than interfaces built for humans.
- It introduces SWE-agent, a system that facilitates LM agents in autonomously using computers to solve software engineering tasks.
- Its named mechanism is a custom agent-computer interface (ACI), which the authors state significantly enhances an agent's ability to create and edit code files, navigate entire repositories, and execute tests and other programs.
- The reported results are a pass@1 rate of 12.5% on SWE-bench and 87.7% on HumanEvalFix, described as state of the art on both and as far exceeding what had been achieved with non-interactive LMs — figures measured in this version of the paper, not standing claims about either benchmark.
- The paper's stated secondary contribution is the insight itself: how the ACI's design affects agent behavior and performance, offered as a finding rather than only as an implementation detail.

## Notes

The paper's contribution is deliberately split between a system and a design claim, and the second
is the one the title carries: interfaces enable the engineering, rather than the agent alone doing
so. The evaluation rests on two benchmarks, SWE-bench and HumanEvalFix, so the reported gains are
bounded by what those two measure. The preprint went through three versions between May and November
2024.
