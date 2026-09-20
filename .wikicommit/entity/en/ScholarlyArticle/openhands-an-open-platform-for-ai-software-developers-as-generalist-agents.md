---
title: "OpenHands: An Open Platform for AI Software Developers as Generalist Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, coding-agents, llm, software-engineering, evaluation, open-source]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2407.16741'
    hash: sha256:01c47d5b7e938859b4b50218e91582dfc7f340a1b2c75d210d80be48372dc1f6
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The arXiv preprint, accepted at ICLR 2025, that introduces OpenHands (formerly OpenDevin) — a platform for building AI agents that interact with the world as a human developer does, by writing code, using a command line and browsing the web."
  author: ["Xingyao Wang", "Boxuan Li", "Yufan Song", "Frank F. Xu", "Xiangru Tang", "Mingchen Zhuge", "Jiayi Pan", "Yueqi Song", "Bowen Li", "Jaskirat Singh", "Hoang H. Tran", "Fuqiang Li", "Ren Ma", "Mingzhang Zheng", "Bill Qian", "Yanjun Shao", "Niklas Muennighoff", "Yizhe Zhang", "Binyuan Hui", "Junyang Lin", "Robert Brennan", "Hao Peng", "Heng Ji", "Graham Neubig"]
  datePublished: "2024-07-23"
  abstract: "The paper introduces OpenHands (formerly OpenDevin), a platform for developing powerful and flexible AI agents that interact with the world in ways similar to a human developer: by writing code, interacting with a command line, and browsing the web. It describes how the platform supports implementing new agents, safe interaction with sandboxed environments for code execution, coordination between multiple agents, and the incorporation of evaluation benchmarks, and reports an evaluation of agents over 15 challenging tasks spanning software engineering and web browsing. OpenHands is released under the permissive MIT license as a community project spanning academia and industry, with more than 2.1K contributions from over 188 contributors."
  keywords: ["Software Engineering (cs.SE)", "Artificial Intelligence (cs.AI)", "Computation and Language (cs.CL)"]
  citation: "arXiv:2407.16741, DOI 10.48550/arXiv.2407.16741"
---

This arXiv preprint introduces [[SoftwareApplication/openhands]], a platform for building AI agents
that act the way a human developer does. Its framing sets two things side by side: software as one
of the most powerful tools humans have, which allows a skilled programmer to interact with the world
in complex and profound ways; and the rapid development, thanks to improvements in large language
models, of AI agents that interact with and affect change in their surrounding environments. The
platform the authors propose joins them — agents that interact with the world in similar ways to
those of a human developer, by writing code, interacting with a command line, and browsing the web.

The body of the paper is a description of what the platform provides. The authors describe how it
allows for the implementation of new agents, safe interaction with sandboxed environments for code
execution, coordination between multiple agents, and the incorporation of evaluation benchmarks.

On the strength of the benchmarks it has incorporated, the authors perform an evaluation of agents
over 15 challenging tasks, which they state include software engineering (giving
[[Dataset/swe-bench]] as an example) and web browsing (giving WebArena as an example), among others.

The paper also states the project's standing as software rather than only as a research artifact:
OpenHands is released under the permissive MIT license and is a community project spanning academia
and industry, with more than 2.1K contributions from over 188 contributors. The preprint is filed
under Software Engineering (cs.SE), with cross-listings to Artificial Intelligence (cs.AI) and
Computation and Language (cs.CL). It was first submitted on 23 July 2024 and last revised on 18
April 2025 as version 3, carries the arXiv-issued DOI 10.48550/arXiv.2407.16741, and is noted as
accepted by ICLR 2025. The code is stated to be at
<https://github.com/All-Hands-AI/OpenHands>.

## Key Points

- The paper introduces OpenHands, formerly known as OpenDevin, as a platform for developing powerful and flexible AI agents.
- Its design goal is agents that interact with the world in similar ways to a human developer — writing code, interacting with a command line, and browsing the web.
- The platform's stated capabilities are implementing new agents, safe interaction with sandboxed environments for code execution, coordination between multiple agents, and incorporation of evaluation benchmarks.
- The authors evaluate agents over 15 challenging tasks drawn from the benchmarks the platform has incorporated, spanning software engineering and web browsing among others.
- OpenHands is released under the permissive MIT license, and the paper characterizes it as a community project spanning academia and industry with more than 2.1K contributions from over 188 contributors — counts that describe the project at the time of writing.
- The paper was accepted by ICLR 2025.

## Notes

The paper's contribution is a platform rather than a single agent, and its evaluation follows from
that: the 15 tasks are described as being drawn from the benchmarks currently incorporated into the
platform, so the reported coverage is a property of what has been integrated as much as of what the
agents can do. The authors give the contribution and contributor counts as evidence of the project's
character as a community effort; both are point-in-time figures. The preprint went through three
versions between July 2024 and April 2025.
