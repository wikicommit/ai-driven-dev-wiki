---
title: "SWE-Compass"
type: "schema:Dataset"
lang: en
tags: [evaluation, agents, coding-agents, benchmarks]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2511.05459'
    hash: sha256:306904f768da56528a41e5c9652823b778a536de3b45569339cba85aa458105c
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An execution-grounded benchmark of 2,000 instances curated from real GitHub pull requests, organised along three orthogonal axes — eight task types, eight programming scenarios and ten programming languages — and used to evaluate the agentic coding abilities of large language models."
  url: "https://huggingface.co/datasets/Kwaipilot/SWE-Compass"
  variableMeasured: ["task type", "programming scenario", "programming language", "number of modified files", "number of changed lines"]
---

SWE-Compass is a benchmark for evaluating the agentic coding abilities of large language models. It
is assembled from authentic GitHub pull requests and organised along three orthogonal axes — task
type, programming scenario and programming language — so that model performance can be diagnosed per
axis rather than reported as a single resolution rate. It was introduced by
[[ScholarlyArticle/swe-compass-towards-unified-evaluation-of-agentic-coding-abilities]], which built
it to address what it describes as the narrow task coverage, language bias and insufficient alignment
with real developer workflows of existing software-engineering benchmarks.

## Contents

One instance pairs a task drawn from a real pull request with an executable environment and
reproducible tests, so that prompting-based and agent-based methods can be compared under controlled
budgets. The benchmark holds 2,000 such instances across 40 repositories, with an average of 4.7
modified files per instance.

The three axes are fixed sets. The **eight task types** are feature implementation, feature
enhancement, bug fixing, refactoring, performance optimisation, code understanding, test case
generation, and configuration and deployment. The **eight programming scenarios** are application
development, database systems, data science and engineering, machine learning and AI, infrastructure
development, specialised programming domains, security engineering, and UI/UX engineering. The **ten
languages** are Python, JavaScript, TypeScript, Java, C, C++, Go, Rust, Kotlin and C#.

The axes were not chosen in advance. The introducing paper derives them from repository-level coding
discussions collected from Stack Overflow and GitHub, using an iterative active-learning procedure:
four popular software-related topics seeded the label pool, an in-context-learning labelling step had
a language model annotate collected conversations along the three dimensions, and tag clustering with
model-guided seed optimisation refined the pool until it converged. Five iterations were performed.

## Provenance

Repositories were filtered on multiple quality indicators — a valid open-source licence, at least 500
stars, active maintenance within the past six months, at least three distinct contributors, more than
1,000 issues and pull requests, more than 200 forks, and the presence of executable unit tests. Pull
requests within those repositories were retained only where they were merged into the main branch,
linked to descriptive issues, carried identifiable file- or line-level changes, and had complete
metadata including repository, issue description, commit, test patch and code patch. About 50,000
pull requests survived that filtering.

Execution environments were then built per pull request by extracting dependency information from
configuration files into Dockerfiles. The paper reports an initial automated build success rate of
around 2%, which expert-assisted repair by 30 annotators raised to roughly 8% retention, producing
about 4,000 runnable images.

Task instances were constructed from those environments by three complementary strategies: checklist
synthesis for code understanding, where model-generated natural-language queries are filtered by a
difficulty-aware scoring function and paired with checklists of key reasoning points; reverse masking
for configuration and deployment and for test case generation, which perturbs verified artifacts —
removing or replacing dependency packages in a Dockerfile, or eliciting incomplete test suites — and
keeps only cases that reproduce a failure; and heuristic filtering for the patch-based task types,
where pull requests are classified by intent and behavioural context, with performance-optimisation
seeds identified as patches that pass unit tests before and after while improving runtime by more
than 30%. A final validation stage applied difficulty filtering, task-balanced sampling weighted to
reflect realistic language distributions, and manual expert verification of executability,
correctness and semantic consistency.

The dataset is published at <https://huggingface.co/datasets/Kwaipilot/SWE-Compass>.

## Use

The introducing paper evaluates ten models under two agentic frameworks, SWE-Agent and Claude Code,
in fixed offline containers with networking disabled and no retries. It reports Claude-Sonnet-4
first under both, at 32.9% macro-average with Claude Code and 31.8% with SWE-Agent, with most scores
clustering in the low-to-mid twenties and the overall range roughly 10-33%. Among open-weight
systems it reports Qwen3-Coder-480B-A35B-Instruct reaching 27.2% with SWE-Agent and 21.9% with Claude
Code.

The same paper uses the benchmark's trajectories for a failure analysis, sampling 600 failed
trajectories per model for three systems and classifying them under a six-category taxonomy. It
reports requirement misinterpretation and incomplete solutions with side effects together accounting
for more than 60% of failures, against 5-8% for technical knowledge gaps.

The paper positions the benchmark against earlier repository-level datasets — its comparison table
lists [[Dataset/swe-bench-verified]], [[Dataset/swe-bench-pro]] and [[Dataset/multi-swe-bench]] among
others — on the grounds that those cover fewer languages and, in most cases, only bug fixing.
