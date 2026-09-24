---
title: "TM-Bench"
type: "schema:Dataset"
lang: en
tags: [benchmarks, evaluation, tool-use]
sources:
  - type: url
    url: 'https://aclanthology.org/2025.acl-long.1266.pdf'
    hash: sha256:e540f7778ba7b71c57f3614b2a333278db9a340b0b059328649725e9e89f3eab
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A benchmark of 15 computational tasks, mostly from medicine and the life sciences, for evaluating agents that turn a scientific code repository into a reusable tool, with held-out test invocations and 124 unit tests to check each tool's correctness."
  url: "https://github.com/KatherLab/ToolMaker"
---

TM-Bench is a benchmark for "tool makers": systems that, given a task and the code repository behind a scientific paper, produce both an environment definition and a tool implementation. It was introduced alongside [[SoftwareApplication/toolmaker]] in [[ScholarlyArticle/llm-agents-making-agent-tools]], and it can evaluate any system that produces those two artifacts. Unlike code-generation benchmarks that assume dependencies are already installed, its tasks run in a fully open-ended environment and cover the whole workflow — downloading resources, resolving dependency problems, reading large codebases, and implementing, testing and debugging code.

## Contents

The benchmark holds 15 tasks. Most come from medical disciplines — pathology, radiology and omics — and the rest from other areas, including 3D vision, imaging, tabular data analysis and natural language processing. They range from tasks that call a single existing method to multi-step tasks that orchestrate several function calls, transform data and use GPUs. Many require external files; one example asks for a biomarker classification model to be trained on a dataset of whole slide images and a clinical data table.

Each task definition gives a one-sentence description, the URL of the code repository, a list of input arguments with one example invocation, and a description of the expected output. The example invocation deliberately omits the expected return value. Each task also has 2–3 held-out test invocations with different input values, 42 in total, and unit tests for each, 124 in total. The tests make assertions about the structure of return values, their values, any files the tool produces, and whether execution errored. A tool counts as correct only if it passes every unit test of its test invocations.

## Provenance

The tasks were curated in close collaboration with researchers in medicine and the life sciences to reflect realistic problems in those fields. Before a task was included, the authors implemented the intended tool themselves from the associated repository, to make sure the task was well defined and solvable. Unit tests were chosen over exact matches against reference outputs so that criteria such as the shape of a feature vector or a plausibly sized segmentation mask could be checked. The unit tests and test invocations are used only for evaluation and are never available during tool creation. The benchmark pins the exact commits of the repositories it references, though the authors note that deletions, force-pushes or renamed branches upstream could still affect reproducibility. The benchmark is published with ToolMaker's code.

## Use

In [[ScholarlyArticle/llm-agents-making-agent-tools]], ToolMaker correctly implemented 12 of the 15 tasks, while an adapted [[SoftwareApplication/openhands]] correctly implemented 3. The authors caution that passing the benchmark's tests does not guarantee correctness in all real-world scenarios, since scientific workflows often involve edge cases that a small set of tests does not capture.
