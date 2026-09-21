---
title: "SWE-Review-Traj"
type: "schema:Dataset"
lang: en
tags: [code-review, agents, training-data]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.06065'
    hash: sha256:cb4fdaa0aecd873bb17c7946eae064e6fc7d82ab88b72e25a69a45f06154657d
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A corpus of agentic code-review trajectories — the exploration traces, evidence, decisions and diagnoses produced by a teacher reviewer working through candidate pull requests — assembled to give open reviewer training data that the authors describe as otherwise scarce."
  variableMeasured: ["exploration trace", "repository evidence gathered", "approve/request-changes decision", "diagnosis text"]
---

SWE-Review-Traj is the training corpus released alongside [[Dataset/swe-review-bench]] in [[ScholarlyArticle/swe-review]]. Where the benchmark measures a reviewer, this dataset is meant to produce one: it records what an agentic reviewer actually did while reaching a verdict, so that a smaller open model can be fine-tuned on that behaviour. The authors present it as filling a gap in the open-source research community, where they describe high-quality trajectories for agentic code review as scarce.

## Contents

A record is one complete review trajectory: the reviewer's exploration of the repository, the evidence it gathered, the binary decision it reached, and the diagnosis it wrote. The released default set contains 8,914 trajectories. A more heavily filtered variant of 6,789 trajectories also exists, and the paper reports that training on it showed no clear benefit over the default.

## Provenance

The issues are sourced from SWE-rebench, filtered to instances with verified solutions, and any instance from a repository appearing in SWE-Review-Bench was excluded to prevent leakage — leaving approximately 6,000 issues. Candidate pull requests were generated with the same three models used to build the benchmark, and after removing empty or oversized patches (over 50KB, which the authors say typically indicate large-scale file deletion rather than a targeted fix) 14,156 candidates remained.

Trajectories were then collected with open-weight GLM-5, thinking enabled, deployed under the OpenHands-SDK scaffold as the teacher — chosen over a closed model, the authors state, so that the traces are complete and transparent. The prompt asks the teacher to understand the issue and trace the root cause before inspecting the pull request, to avoid biasing the review toward the candidate's proposed fix. One review per candidate yielded 14,156 raw trajectories, which decision-correctness filtering — keeping only trajectories that correctly approve a resolving patch or correctly request changes on a non-resolving one — reduced to the released 8,914.

The authors audited diagnosis quality rather than assuming it. Two proprietary judges rated factual accuracy, fix correctness and grounding on a 1–5 scale, returning means just above 3.0 with substantial agreement (Cohen's κ = 0.72) and only 3.3% of paired ratings differing by two points or more. They read this as evidence the diagnoses carry meaningful valid information while explicitly not claiming they are correct.

## Use

[[ScholarlyArticle/swe-review]] reports that supervised fine-tuning an 8B model on this corpus raised its completion rate from approximately 4% to 71–84% and its decision accuracy from near-random to 67–72%, and that mixing these trajectories with issue-resolution training data improved direct resolve rate by up to 5.6 points while producing a unified generate-review-revise agent with up to a 10.6-point gain in final resolve rate.
