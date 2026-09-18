---
title: "SWE-Bench"
type: "schema:Dataset"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2508.11126'
    hash: sha256:d8a0f4c103987a46e21f37fca41b5ebfa795945e9c798921c4fdfbfc18bd9346
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A benchmark built from real GitHub issues that evaluates whether language models and coding agents can resolve Python software-engineering tasks, using unit tests and continuous integration to check correctness."
  variableMeasured: ["task type", "proportion", "interaction type", "multi-turn feedback", "library integration", "build pipeline"]
---

SWE-Bench is a benchmark built from real GitHub issues, used to evaluate whether language models and coding agents can resolve software-engineering tasks in Python repositories. Task correctness is checked using unit tests and continuous integration (CI).

## Contents

The survey characterizes SWE-Bench's task mix as split across three levels of scope: function-level tasks (65% of tasks), checked only against unit tests; module-level tasks (25%), checked against tests and CI; and project-level tasks (under 10%), also checked against tests and CI but with only limited, pass/fail multi-turn interaction. None of the three task types involve third-party library integration or build-pipeline management in the survey's characterization.

## Provenance

The benchmark's tasks are sourced from GitHub issues. The survey separately lists SWE-Bench Multimodal, a related benchmark that uses JavaScript rather than Python, as a distinct dataset from SWE-Bench itself. [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] describes a further progression from SWE-Bench to [[Dataset/swe-bench-verified]], a human-validated 500-task subset OpenAI released with the SWE-Bench authors to address concerns that some tasks were ambiguous or underspecified, and then to [[Dataset/swe-bench-pro]], which OpenAI recommended after SWE-Bench Verified became increasingly exposed to data contamination.

## Use

The survey cites SWE-Bench as an example of the broader benchmarking gap it identifies: it introduces project-level repositories and leverages unit tests and CI for evaluation, yet its scope is restricted to Python, most of its tasks are function- or module-level, and even its project-level tasks provide only minimal support for the realistic multi-turn, tool-integrated software engineering workflows that practical agentic systems are expected to handle.

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] cites several deeper examinations of SWE-Bench results as showing that passing tests alone is not enough to establish that agent-generated code is merge-ready for professional codebases: 29.6% of "plausible" fixes were found to introduce behavioral regressions or be incorrect upon rigorous retesting; true solve rates for GPT-4 patches dropped from 12.47% to 3.97% after detailed manual audits revealed widespread weak or cosmetic solutions; AI agents frequently produced superficial patches limited to single files, unlike human developers; and many patches that passed unit tests failed broader CI checks due to style or hidden regressions.
