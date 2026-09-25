---
title: "FeatureBench"
type: "schema:Dataset"
lang: en
tags: [benchmarks, evaluation, coding-agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2602.10975'
    hash: sha256:41a29ebab57dc2c90294974e352929b6c0d4706053fdba87e2ee97ba915b22f2
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A benchmark of feature-level coding tasks for LLM agents, derived automatically from Python repositories, whose first version contains 200 evaluation tasks and 3825 executable environments from 24 open-source GitHub repositories."
  variableMeasured: ["instance_id", "patch", "test_patch", "FAIL_TO_PASS", "PASS_TO_PASS", "image_name", "repo", "base_commit", "problem_statement", "repo_settings"]
---

FeatureBench is a benchmark for evaluating coding agents on end-to-end, feature-oriented software
development: implementing a new capability either inside an existing codebase or as a standalone
module, given a task description and explicit interface definitions. It was introduced in
[[ScholarlyArticle/featurebench-benchmarking-agentic-coding-for-complex-feature-development]] as a
harder, feature-focused counterpart to [[Dataset/swe-bench]].

## Contents

Each task instance records a unique identifier, the gold patch and the test patch, the lists of
fail-to-pass and pass-to-pass test files, the Docker image for the development environment, the
source repository and base commit, the problem statement, and the repository settings. A generated
instance directory holds the task prompt (`problem_statement.md`), the gold patch, the test patch
and a metadata file. The problem statement has two parts, a task description and interface
descriptions giving the path, signature and docstring of each interface to implement.

The first version contains 200 evaluation tasks, selected from 3825 executable environments across
24 Python repositories from domains such as machine learning, scientific computing, visualization
and web frameworks; mlflow, transformers and pandas contribute the most tasks. Inclusion in the full
set required more than 100 lines of code to implement, at least 10 fail-to-pass test points, and
test files first committed after May 2022. A Lite set of 30 randomly chosen tasks is provided to
reduce evaluation cost. Every task exists at two difficulty levels: Level 1 (incremental
development within the repository) and Level 2 (the same functionality built from scratch, with the
repository removed). Compared with a SWE-bench instance, an average task has a far longer problem
statement and a gold solution touching many more lines, files and functions, with many more tests to
pass.

## Provenance

The tasks were produced by the paper's automated, test-driven collection toolkit. For each
repository, installation commands are specified by hand — the only manual step, estimated at about
three minutes per repository — and the environment is packaged as a Docker image. The toolkit
selects validated test files as fail-to-pass and pass-to-pass tests, traces their execution to build
a function-level dependency graph, uses an LLM to classify which imported objects are the tested
targets, and extracts the target feature by breadth-first traversal while keeping code exercised by
pass-to-pass tests. A post-verification step checks the stripped codebase before a problem
statement is generated, with an LLM filling in missing docstrings. The tasks were created from
repository activity between May 2022 and September 2025, and the authors describe the benchmark as
continually updatable because the same toolkit can generate new instances over time. The code is
published on GitHub under LiberCoders/FeatureBench.

## Use

The introducing paper evaluated seven agent scaffold and model combinations on the benchmark and
reports that the best resolved only 12.5% of the full set; its results are summarized on the paper's
page.
