---
title: "From LLMs to LLM-based Agents for Software Engineering: A Survey of Current, Challenges and Future"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, surveys, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2408.02479'
    hash: sha256:69e3a7c17da563fb19e960cd8533593e4c71f9a2152f67ca1199377629babed0
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A survey of 139 papers on large language models and LLM-based agents in software engineering, organised into six topics and comparing the two paradigms topic by topic on tasks, benchmarks and evaluation metrics. It proposes six criteria for deciding when an LLM architecture qualifies as an agent, and analyses the models, benchmarks and metrics used across the collected experiments."
  author: ["Haolin Jin", "Linghan Huang", "Haipeng Cai", "Jun Yan", "Bo Li", "Huaming Chen"]
  abstract: "The survey investigates current practice and solutions for both LLMs and LLM-based agents in software engineering, motivated by the observation that existing surveys do not clearly distinguish the two and that no unified standard or benchmark yet qualifies an LLM solution as an agent in its domain. It summarises six key topics — requirement engineering and documentation, code generation and software development, autonomous learning and decision-making, software design and evaluation, test generation, and software maintenance — reviewing and differentiating LLM and LLM-based agent work within each on tasks, benchmarks and evaluation metrics, and then analyses the models and benchmarks used across the collected literature."
  keywords: ["Large Language Models", "LLM-based Agents", "Software Engineering", "Benchmark", "Software Security", "AI System Development"]
---

This paper surveys the transition from large language models to LLM-based agents across software
engineering. Its stated motivation is that although many studies explore LLMs in software
engineering, they lack a clear distinction between LLMs and LLM-based agents, and that the field is
still at an early stage for a unified standard or benchmark that would qualify an LLM solution as an
agent. The authors organise software engineering into six topics — requirement engineering and
documentation, code generation and software development, autonomous learning and decision making,
software design and evaluation, software test generation, and software security and maintenance —
and treat each one twice, once for plain LLM approaches and once for agent-based ones.

The corpus was assembled from DBLP and arXiv, covering publications from the latter half of 2023 to
December 2024, using keyword clusters combined with Boolean operators and a snowballing pass over
the references of retained papers. The paper states its inclusion criteria (the work must explicitly
involve LLMs, be relevant to software engineering tasks, and provide sufficient experimental results)
and its exclusion criteria (papers under seven pages, general-AI work unrelated to LLMs, work that
does not address software engineering applications or workflows, grey literature such as blog posts
and whitepapers, duplicates, and papers not written in English). The result is 139 papers; the paper
notes that some address several topics at once, so the per-topic counts sum to more than 139. Of
these, it reports that 40.3% appeared on arXiv and 59.7% in established peer-reviewed venues, with
NeurIPS (10.1%) and ICSE (6.5%) the largest single venues.

Each topic chapter follows the same structure — LLM tasks, LLM-based agent tasks, an analysis
contrasting the two, the benchmark datasets each paradigm uses, and the evaluation metrics each
reports — and the survey closes with a cross-topic discussion of the experiment models, the
topic overlaps, the benchmarks and metrics, and a set of challenges and research opportunities.

## Key Points

- The survey proposes six criteria for treating an LLM architecture as an agent: the LLM serves as
  the brain; the framework has decision-making and planning abilities beyond language understanding
  and generation; the model can autonomously decide when and which tools to use and integrate the
  results; it can select the optimal solution among several homogeneous results; it can handle
  multiple interactions while maintaining contextual understanding; and it has autonomous learning
  and adaptability. The authors treat the first four as fundamental to a basic level of agency and
  the last two as more advanced but not strictly necessary, and state that a framework qualifies if
  it meets most of them. The criteria are the authors' own synthesis of mainstream definitions and
  first-half-2024 literature, not a settled community standard — the survey states plainly that no
  consensus exists on the level of autonomy, planning capability and tool usage required.
- The two paradigms attract research attention in different places. Among the LLM papers, requirement
  engineering and documentation is the most represented topic, followed closely by software security
  and maintenance, and the two together account for nearly half. Among the agent papers, autonomous
  learning and decision making is the most prominent at nearly 30%, followed by code generation and
  development, while requirement engineering and test case generation remain comparatively thin.
- Evaluation metrics diverge along the same line. The survey's top-ten tally gives accuracy (20.9%),
  pass rate (16.4%), F1 score (11.9%), correctness (11.9%) and exact match (6.0%) as the most common
  LLM metrics, and success rate (20.0%), accuracy (15.7%) and pass@1 (12.9%) as the most common agent
  metrics, with agent-specific additions for efficiency (5.7%), win rate (4.5%), cost (4.3%) and
  correctness rate (4.3%). The authors read this as agents being judged on end-to-end, multi-step
  success and on resource consumption, where LLMs are judged on static classification or generation
  correctness.
- Benchmark usage diverges too. HumanEval and MBPP are the most widely adopted across both paradigms,
  while agent studies additionally reach for benchmarks supporting interactive or knowledge-intensive
  reasoning such as HotpotQA, FEVER, ALFWorld and WebShop. The survey observes that Defects4J remains
  a staple for LLM code-repair evaluation but is rarely used by agent studies, and attributes this to
  its focus on single-step repair being poorly aligned with multi-turn, tool-augmented systems.
- Across the 139 papers the survey identifies 82 distinct large language models used in experiments,
  and reports GPT-3.5, GPT-4, LLaMA2 and Codex as the most frequent. It observes that agent studies
  use a narrower variety of models than LLM studies, which it attributes to agents needing a
  general-purpose core with strong text comprehension for reasoning, planning and execution rather
  than a model specialised for one task.
- It names six open challenges: the absence of standardised agent definitions and evaluation
  protocols; workflow complexity and error propagation in multi-agent systems; tool-integration
  bottlenecks and external dependency management; the lack of cross-task generalisation and knowledge
  transfer; data scarcity and insufficient simulation environments for evaluating agent behaviour;
  and cognitive transparency and trustworthiness as autonomy increases.

## Notes

The survey positions itself against earlier reviews of LLMs in software engineering by adding the
LLM-versus-agent distinction as an explicit axis and by confining its corpus to a narrow, recent
window, on the argument that earlier surveys span a wide range of publication dates and therefore
give uneven coverage of topics whose literature grew quickly. Its own stated limitations follow from
the same choices: the corpus is drawn from two databases, the cut-off is December 2024, and the
per-topic counts double-count papers that address more than one topic.

For the concept the survey's criteria are proposed about, see [[DefinedTerm/ai-agent]]; for the
narrower category most of its code-generation chapter concerns, see [[DefinedTerm/ai-coding-agent]].
