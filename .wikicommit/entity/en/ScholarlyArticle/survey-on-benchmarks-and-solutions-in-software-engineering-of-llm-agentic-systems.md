---
title: "A Comprehensive Survey on Benchmarks and Solutions in Software Engineering of LLM-Empowered Agentic System"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, software-engineering, benchmarks, survey]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2510.09721'
    hash: sha256:e49c71ec59249d2c7e0b86eb0c2633db32838a157261a7cf6153937981444be0
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A survey of over 150 papers on LLM-powered software engineering, proposing a taxonomy along two dimensions — solutions (prompt-based, fine-tuning-based, agent-based) and benchmarks — and connecting 50+ benchmarks to the solution strategies that address them."
  author: ["Jiale Guo", "Suizhi Huang", "Mei Li", "Dong Huang", "Xingsheng Chen", "Regina Zhang", "Zhijiang Guo", "Han Yu", "Siu-Ming Yiu", "Pietro Lio", "Kwok-Yan Lam"]
  datePublished: "2025-10-10"
  keywords: ["Software Engineering", "Computation and Language"]
  citation: "arXiv:2510.09721"
---

This survey addresses what its authors describe as a lack of comprehensive understanding of how
benchmarks and solutions in LLM-powered software engineering interconnect. It frames the field as
having moved from traditional rule-based systems to autonomous agentic systems capable of solving
complex problems, and offers what it presents as the first holistic analysis of the area, covering
both evaluation methodologies and solution paradigms.

The review covers over 150 recent papers and organizes them along two dimensions. Solutions are
categorized into prompt-based, fine-tuning-based, and agent-based paradigms; benchmarks are
organized by task, including code generation, translation, and repair. The authors describe the
field's trajectory as an evolution from simple [[DefinedTerm/prompt-engineering]] to agentic
systems incorporating planning, reasoning, memory mechanisms, and tool augmentation.

To place that progress in context, the survey presents a unified pipeline illustrating the workflow
from task specification through to deliverables, and details how the different solution paradigms
address varying levels of complexity. The authors maintain a GitHub repository that continuously
updates the reviewed and related papers, at <https://github.com/lisaGuojl/LLM-Agent-SE-Survey>.

## Key Points
- Reviews over 150 recent papers on LLM-powered software engineering and proposes a two-dimensional
  taxonomy: solutions (prompt-based, fine-tuning-based, agent-based) and benchmarks (tasks such as
  code generation, translation, and repair)
- Connects 50+ benchmarks to their corresponding solution strategies, which the authors present as
  the distinguishing contribution over prior surveys that focus narrowly on specific aspects
- Characterizes the field's evolution as running from prompt engineering to agentic systems that
  add planning, reasoning, memory mechanisms, and tool augmentation
- Presents a unified pipeline from task specification to deliverables, mapping solution paradigms
  onto complexity levels
- Identifies research gaps and proposes future directions including multi-agent collaboration,
  self-evolving systems, and formal verification integration

## Notes

The paper is a survey rather than a primary study: its claims are about the shape of the literature
it reviews, not about measured outcomes of its own. Its stated positioning against prior surveys is
the benchmark-to-solution mapping — earlier surveys, in the authors' account, treat evaluation and
solution design separately.

The version summarized here is v3 (23 October 2025); the first version was submitted on 10 October
2025.
