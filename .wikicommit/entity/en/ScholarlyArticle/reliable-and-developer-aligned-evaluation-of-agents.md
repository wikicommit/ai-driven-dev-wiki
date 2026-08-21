---
title: "Reliable and Developer-Aligned Evaluation of Agents for Software Engineering"
type: "schema:ScholarlyArticle"
lang: en
tags: [evaluation, benchmark, agentic-coding, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/html/2607.06713v1'
    hash: sha256:8710bde95207c8a2182830337fd263be367d583741958b441b085771e928d2c4
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A research plan presented at FSE '26 arguing that current evaluation practice for LLMs in software engineering is unreliable, hard to reproduce, and poorly aligned with developer needs. It proposes three steps: a systematic review of the evaluation landscape, in-the-wild study of agent behaviour, and a contamination-aware, change-responsive benchmark."
  author:
    - "Razvan Mihai Popescu"
  datePublished: "2026-07-07"
  keywords:
    - "evaluation"
    - "benchmarking"
    - "data contamination"
---

This is a research plan by Razvan Mihai Popescu of Delft University of Technology, published in the Companion Proceedings of the 34th ACM Symposium on the Foundations of Software Engineering (FSE '26) and posted to arXiv on 7 July 2026.

Its critique is of measurement practice rather than of any model or agent: "current evaluation practices are often unreliable, difficult to reproduce, and poorly aligned with real-world developer needs," relying heavily on convenience-based metrics. The consequence it names is not merely inaccuracy but distortion — these practices "often creat[e] an illusion of model competence," resulting in "misleading conclusions and potentially harmful downstream" effects, and they remain the norm regardless.

Its account of why the established benchmarks fall short is specific: HumanEval, MBPP, and Defects4J "provide reproducible measures of functional correctness, yet are known to suffer from saturation, data contamination, and limited contextual realism," with leaderboards reporting near-ceiling performance. It also distinguishes coding agents from their predecessors on grounds that matter for evaluation — agents "not only add a layer of autonomy and persistence over their precedents, but they are also capable of adjusting their behavior in response to observed effects," which a static benchmark cannot capture.

## Key Contributions

The plan sets out three steps.

- **Evaluation landscape.** A systematic literature review synthesizing 279 peer-reviewed papers across 26 coding tasks, asking which LLMs have been evaluated on code-related tasks, what datasets drive those evaluations, and what evaluation techniques have been applied.
- **In-the-wild evaluation.** Using the fact that specialized coding agents — it names OpenAI Codex, [[SoftwareApplication/github-copilot]], [[SoftwareApplication/claude-code]], and [[SoftwareApplication/jules]] — operate inside development environments and manipulate version control, this step studies agent behaviour where it actually happens. Its questions are how agent-authored activity differs from human-authored activity in shaping collaboration and development progress, and how agent-authored contributions influence the trajectory of code maintenance over time compared with human ones.
- **Change-responsive evaluation.** A multilingual, contamination-aware benchmark for end-to-end issue resolution in evolving software repositories, built on the observation that real development "unfolds through evolving requirements, iterative changes, and collaborative decision-making, shaping the trajectory of codebases over time" — that is, evaluating an agent against change rather than against a fixed task snapshot.

## Notes

This is a research plan rather than a completed study, but not uniformly prospective: the systematic review is reported as conducted, and the in-the-wild step is described as performed too — with a thorough analysis of agentic and human development activity, a longitudinal investigation of its impact on codebase maintainability and failure points, and the release of a large-scale dataset of agentic and human contributions. Only the change-responsive benchmark is stated purely as future work. What it contributes to this wiki now is a well-organised statement of the measurement problem, from inside the software engineering research community, at a moment when benchmark figures are the main currency of claims about agent capability.

Its three criticisms of the established benchmarks are worth holding alongside the numbers recorded elsewhere here. Saturation and contamination are the same cautions the sources on [[Dataset/swe-bench]] raise about that benchmark's Verified subset, and the "illusion of model competence" framing gives a name to what happens when a single headline trajectory — such as the 1.96%-to-78.4% figure reported in [[ScholarlyArticle/agentic-ai-in-the-software-development-lifecycle]] — stands in for capability. The plan's move toward evaluating agents inside real version-control activity converges with the approach already taken by [[ScholarlyArticle/security-in-the-age-of-ai-teammates]] and by the harness-focused measurement in [[ScholarlyArticle/dont-blame-the-large-language-model]], both of which find things a task benchmark does not surface.
