---
title: "A Survey on Evaluation of LLM-based Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, evaluation, benchmarks]
sources:
  - type: url
    url: 'https://aclanthology.org/2026.findings-acl.1330/'
    hash: sha256:87c6c3ed65ef518f7d882cffec88399e0c5382682206e0e9407a368a58180c94
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A survey of evaluation methods for LLM-based agents, presented at Findings of ACL 2026, that organizes the field across five perspectives — core agentic capabilities, application-specific benchmarks, generalist agents, benchmark design dimensions, and developer-facing evaluation frameworks — and identifies gaps in assessing cost-efficiency, safety and robustness."
  author: ["Asaf Yehudai", "Lilach Eden", "Alan Li", "Guy Uziel", "Yilun Zhao", "Roy Bar-Haim", "Arman Cohan", "Michal Shmueli-Scheuer"]
  datePublished: "2026-07"
  abstract: "The paper surveys how LLM-based agents are evaluated, covering the core LLM capabilities agentic workflows depend on (such as planning and tool use), application-specific benchmarks including web and SWE agents, the evaluation of generalist agents, the core dimensions along which agent benchmarks are built, and the evaluation frameworks and tools available to agent developers. The authors report a shift toward more realistic and challenging evaluations with continuously updated benchmarks, and identify cost-efficiency, safety and robustness as areas where assessment is still weak."
---

This paper is a survey of evaluation methods for LLM-based agents, published in *Findings of the Association for Computational Linguistics: ACL 2026*. Its starting position is that LLM-based agents represent a paradigm shift in AI: systems that plan, reason and use tools autonomously while interacting with dynamic environments. The authors describe their survey as the first comprehensive treatment of how such agents are evaluated.

The survey organizes the field of agent evaluation into five perspectives. The first covers the core LLM capabilities that agentic workflows depend on, naming planning and tool use as examples. The second covers application-specific benchmarks, including those for web agents and for SWE (software engineering) agents. The third covers the evaluation of generalist agents, the fourth analyses the core dimensions along which agent benchmarks are constructed, and the fifth surveys the evaluation frameworks and tools available to agent developers.

From that analysis the authors report a trend in the field toward more realistic and more challenging evaluations, supported by benchmarks that are continuously updated rather than fixed at release. They also name the gaps they consider most critical for future work.

## Key Points

- The survey presents itself as the first comprehensive survey of evaluation methods for LLM-based agents.
- It analyses agent evaluation across five perspectives: core LLM capabilities needed for agentic workflows, application-specific benchmarks, evaluation of generalist agents, analysis of agent benchmarks' core dimensions, and evaluation frameworks and tools for agent developers.
- Web agents and SWE agents are named as the application-specific benchmark categories the survey examines.
- The authors report a trend toward more realistic, more challenging evaluations built on continuously updated benchmarks.
- They identify cost-efficiency, safety and robustness as the dimensions current agent evaluation assesses least well.
- They also call for fine-grained, scalable evaluation methods, which they treat as an open problem rather than a solved one.

## Notes

The gaps the authors name — cost-efficiency, safety, robustness, and fine-grained scalable evaluation — are stated as directions future research must address rather than as findings the survey itself settles. The paper appears in the Findings track of ACL 2026 and is published by the Association for Computational Linguistics under DOI 10.18653/v1/2026.findings-acl.1330.
