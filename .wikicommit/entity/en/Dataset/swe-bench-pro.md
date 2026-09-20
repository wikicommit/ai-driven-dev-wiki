---
title: "SWE-Bench Pro"
type: "schema:Dataset"
lang: en
tags: [evaluation, coding-agents, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
  - type: url
    url: 'https://arxiv.org/abs/2509.16941'
    hash: sha256:b91dc52045b9c4439615f96ff2d063a26d56023a0a8d46564996bf7bd7a789a6
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A contamination-resistant benchmark of 1,865 long-horizon, enterprise-level software engineering problems drawn from 41 actively maintained repositories, partitioned into a public set, a held-out set and a commercial set of proprietary repositories."
  url: "https://doi.org/10.48550/ARXIV.2509.16941"
---

SWE-Bench Pro is a benchmark for evaluating whether AI agents can solve long-horizon software
engineering tasks. The paper that introduces it,
[[ScholarlyArticle/swe-bench-pro-can-ai-agents-solve-long-horizon-software-engineering-tasks]],
presents it as building upon the best practices of [[Dataset/swe-bench]] while being explicitly
designed to capture realistic, complex, enterprise-level problems beyond that benchmark's scope.

## Contents

The introducing paper gives the benchmark as 1,865 problems sourced from a diverse set of 41
actively maintained repositories spanning business applications, B2B services and developer tools.
Those repositories are partitioned three ways: a public set with open access to problems sourced
from 11 repositories, a held-out set of 12 repositories, and a commercial set of 18 proprietary
repositories. Problems in the held-out and commercial sets are not publicly accessible, though the
authors state they release results on the commercial set.

The introducing paper describes the benchmark's tasks as
long-horizon ones that may require hours to days for a professional software engineer to complete,
often involving patches across multiple files and substantial code modifications. All tasks are
stated to be human-verified and augmented with sufficient context to ensure resolvability.

## Provenance

The 41 repositories the problems are sourced from are described as actively maintained. The 18
repositories of the commercial partition are proprietary, and the introducing paper states the
authors hold formal partnership agreements with early-stage startups covering them; problems in that
partition and in the held-out partition are not publicly accessible. The authors summarize the
benchmark as a contamination-resistant testbed that more faithfully captures the complexity and
diversity of real-world software development.

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] traces a progression from
[[Dataset/swe-bench]] to [[Dataset/swe-bench-verified]] to SWE-Bench Pro, calling it evidence of both
the field's rapid progress and the difficulty of maintaining uncontaminated measures of agent
capability. That paper describes SWE-Bench Pro as the benchmark OpenAI recommended in place of
SWE-Bench Verified after that benchmark became increasingly exposed to data contamination.

## Use

The introducing paper reports an analysis of how agents fail on the benchmark rather than a headline
score: the authors cluster the failure modes observed in the collected agent trajectories, in order
to arrive at a clearer characterization of the error patterns exhibited by current models.
