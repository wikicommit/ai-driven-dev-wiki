---
title: "SWE-Bench Pro: Can AI Agents Solve Long-Horizon Software Engineering Tasks?"
type: "schema:ScholarlyArticle"
lang: en
tags: [evaluation, coding-agents, llm, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2509.16941'
    hash: sha256:b91dc52045b9c4439615f96ff2d063a26d56023a0a8d46564996bf7bd7a789a6
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The arXiv preprint that introduces SWE-Bench Pro, a contamination-resistant benchmark of 1,865 long-horizon, enterprise-scale software engineering problems drawn from 41 actively maintained repositories and split into public, held-out and commercial sets."
  author: ["Xiang Deng", "Jeff Da", "Edwin Pan", "Yannis Yiming He", "Charles Ide", "Kanak Garg", "Niklas Lauffer", "Andrew Park", "Nitin Pasari", "Chetan Rane", "Karmini Sampath", "Maya Krishnan", "Srivatsa Kundurthy", "Sean Hendryx", "Zifan Wang", "Vijay Bharadwaj", "Jeff Holm", "Raja Aluri", "Chen Bo Calvin Zhang", "Noah Jacobson", "Bing Liu", "Brad Kenstler"]
  datePublished: "2025-09-21"
  abstract: "The paper introduces SWE-Bench Pro, a substantially more challenging benchmark that builds on the best practices of SWE-bench but is explicitly designed to capture realistic, complex, enterprise-level problems beyond its scope. It contains 1,865 problems from 41 actively maintained repositories spanning business applications, B2B services and developer tools, partitioned into a public set of 11 repositories, a held-out set of 12, and a commercial set of 18 proprietary repositories held under formal partnership agreements with early-stage startups. The tasks are long-horizon — potentially hours to days of work for a professional engineer, often requiring patches across multiple files — and all are human-verified and augmented with sufficient context to ensure resolvability. The authors also cluster the failure modes observed in collected agent trajectories to characterize current models' error patterns."
  keywords: ["Software Engineering (cs.SE)", "Computation and Language (cs.CL)"]
  citation: "arXiv:2509.16941, DOI 10.48550/arXiv.2509.16941"
---

This arXiv preprint introduces [[Dataset/swe-bench-pro]], presented as a substantially more
challenging benchmark that builds upon the best practices of [[Dataset/swe-bench]] while being
explicitly designed to capture realistic, complex, enterprise-level problems beyond that benchmark's
scope.

The paper gives the benchmark's composition in detail. It contains 1,865 problems sourced from a
diverse set of 41 actively maintained repositories spanning business applications, B2B services and
developer tools, and is partitioned three ways: a public set with open access to problems sourced
from 11 repositories; a held-out set of 12 repositories; and a commercial set of 18 proprietary
repositories, which the authors state they hold under formal partnership agreements with early-stage
startups. Problems in the held-out and commercial sets are not publicly accessible, though the
authors state they release results on the commercial set.

What distinguishes the tasks is their length. The authors describe the benchmark as featuring
long-horizon tasks that may require hours to days for a professional software engineer to complete,
often involving patches across multiple files and substantial code modifications. They also state
that all tasks are human-verified and augmented with sufficient context to ensure resolvability — so
that a failure is a failure of the agent rather than of the task's specification.

Alongside the benchmark the authors report an analysis of how agents fail on it: to better
understand the limitations they observe, they cluster the failure modes found in the collected agent
trajectories, for what they describe as a clearer characterization of the error patterns exhibited
by current models. They summarize the whole as a contamination-resistant testbed that more
faithfully captures the complexity and diversity of real-world software development, advancing the
pursuit of truly autonomous software engineering agents at a professional level.

The preprint is filed under Software Engineering (cs.SE), with a cross-listing to Computation and
Language (cs.CL). It was first submitted on 21 September 2025 and revised on 14 November 2025 as
version 2, and carries the arXiv-issued DOI 10.48550/arXiv.2509.16941.

## Key Points

- The paper introduces SWE-Bench Pro as a substantially more challenging benchmark that builds on SWE-bench's best practices while targeting enterprise-level problems beyond its scope.
- The benchmark holds 1,865 problems from 41 actively maintained repositories spanning business applications, B2B services and developer tools.
- It is partitioned into a public set (11 repositories), a held-out set (12 repositories) and a commercial set (18 proprietary repositories held under formal partnership agreements with early-stage startups); the latter two are not publicly accessible, though results on the commercial set are released.
- Its tasks are long-horizon: the authors state they may require hours to days of work from a professional software engineer, and often involve patches across multiple files and substantial code modifications.
- All tasks are human-verified and augmented with sufficient context to ensure resolvability.
- The authors cluster the failure modes observed in collected agent trajectories in order to characterize the error patterns current models exhibit.
- The authors summarize the result as a contamination-resistant testbed that more faithfully captures the complexity and diversity of real-world software development.

## Notes

Two of the benchmark's three partitions are stated to be outside public access, and the commercial
set exists at all because of formal partnership agreements with early-stage startups. The
human-verification and sufficient-context conditions are stated as guarantees about resolvability,
which bounds what a low score on this benchmark can be read to mean. The preprint went through two
versions between September and November 2025.
