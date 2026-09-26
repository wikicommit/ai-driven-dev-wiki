---
title: "SWE-Bench"
type: "schema:Dataset"
lang: en
tags: [evaluation, agents, coding-agents, leaderboards]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2508.11126'
    hash: sha256:d8a0f4c103987a46e21f37fca41b5ebfa795945e9c798921c4fdfbfc18bd9346
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
  - type: url
    url: 'https://arxiv.org/abs/2310.06770'
    hash: sha256:706b494065faa4145cd8f13923309b0192bd91ae7eac0d5f62df2ceaacb70416
  - type: url
    url: 'https://www.swebench.com/'
    hash: sha256:80c659d8a196c9dac19e7364704397cbd136cc0d9416d332a9702948b5d55fe8
review_status: reviewed
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A benchmark built from real GitHub issues that evaluates whether language models and coding agents can resolve Python software-engineering tasks, using unit tests and continuous integration to check correctness."
  url: "https://www.swebench.com"
  variableMeasured: ["task type", "proportion", "interaction type", "multi-turn feedback", "library integration", "build pipeline"]
reviewed_by: "joyk0117"
---

SWE-Bench is a benchmark built from real GitHub issues, used to evaluate whether language models and
coding agents can resolve software-engineering tasks in Python repositories. Task correctness is
checked using unit tests and continuous integration (CI).

## Contents

[[ScholarlyArticle/swe-bench-can-language-models-resolve-real-world-github-issues]], the paper that
introduces the benchmark, gives its scale as 2,294 software engineering problems drawn from real
GitHub issues and the corresponding pull requests, across 12 popular Python repositories. One
problem presents a codebase together with a description of an issue to be resolved, and the model
under evaluation must edit the codebase to address it. That paper characterizes the work the format
demands as coordinating changes across multiple functions, classes and even files simultaneously,
interacting with execution environments, processing extremely long contexts, and reasoning beyond
traditional code generation.

The survey characterizes SWE-Bench's task mix as split across three levels of scope: function-level tasks (65% of tasks), checked only against unit tests; module-level tasks (25%), checked against tests and CI; and project-level tasks (under 10%), also checked against tests and CI but with only limited, pass/fail multi-turn interaction. None of the three task types involve third-party library integration or build-pipeline management in the survey's characterization.

## Provenance

The benchmark's tasks are sourced from GitHub issues, taken together with the pull requests that
correspond to them. Data, code and a leaderboard are stated by the introducing paper to be available
at <https://www.swebench.com>.

The survey separately lists SWE-Bench Multimodal, a related benchmark that uses JavaScript rather than Python, as a distinct dataset from SWE-Bench itself. [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] describes a further progression from SWE-Bench to [[Dataset/swe-bench-verified]], a human-validated 500-task subset OpenAI released with the SWE-Bench authors to address concerns that some tasks were ambiguous or underspecified, and then to [[Dataset/swe-bench-pro]], which OpenAI recommended after SWE-Bench Verified became increasingly exposed to data contamination.

## Benchmark Family and Leaderboards

The benchmark's own site hosts official leaderboards for several members of what it presents as a
family of benchmarks, each reporting a model's **% Resolved** — the percentage of task instances
solved — and marking open-weights models and runs performed or directly checked by the SWE-bench team.
The site lists the members with their sizes:

- **SWE-bench** (the full, original benchmark): 2,294 instances, real GitHub issues from 12 Python
  repositories.
- **SWE-bench Lite**: 300 instances, a subset curated for less costly evaluation, released in March 2024.
- **[[Dataset/swe-bench-verified]]**: 500 instances, a human-filtered subset of SWE-bench, announced in
  August 2024 as a collaboration with [[Organization/openai]].
- **Bash Only**: the default view of the Verified leaderboard, over the same 500 instances, in which
  every model runs in the same [[SoftwareApplication/mini-swe-agent]] environment.
- **SWE-bench Multilingual**: 300 instances, tasks from 42 repositories across 9 programming languages.
- **[[Dataset/swe-bench-multimodal]]**: 480 instances, issues described with visual elements, introduced
  in October 2024.

The site's news list also records that SWE-bench was Docker-ized in June 2024 for easier evaluation.
Alongside the benchmarks, the site groups related tools and evaluations under the same family,
including [[SoftwareApplication/swe-agent]], mini-SWE-agent, SWE-smith (for training models for
software engineering agents), SWE-ReX, a SWE-bench CLI, and the later evaluations CodeClash and
ProgramBench.

## Use

At the time the introducing paper was written, results on the benchmark were low: it reports that
both state-of-the-art proprietary models and the authors' own fine-tuned SWE-Llama resolve only the
simplest issues, with the best-performing model, Claude 2, solving 1.96% of the issues. The authors
frame advances on SWE-Bench as steps towards language models that are more practical, intelligent
and autonomous.

The survey cites SWE-Bench as an example of the broader benchmarking gap it identifies: it introduces project-level repositories and leverages unit tests and CI for evaluation, yet its scope is restricted to Python, most of its tasks are function- or module-level, and even its project-level tasks provide only minimal support for the realistic multi-turn, tool-integrated software engineering workflows that practical agentic systems are expected to handle.

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] cites several deeper examinations of SWE-Bench results as showing that passing tests alone is not enough to establish that agent-generated code is merge-ready for professional codebases: 29.6% of "plausible" fixes were found to introduce behavioral regressions or be incorrect upon rigorous retesting; true solve rates for GPT-4 patches dropped from 12.47% to 3.97% after detailed manual audits revealed widespread weak or cosmetic solutions; AI agents frequently produced superficial patches limited to single files, unlike human developers; and many patches that passed unit tests failed broader CI checks due to style or hidden regressions.
