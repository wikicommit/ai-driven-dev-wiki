---
title: "LoopsBench"
type: "schema:Dataset"
lang: en
tags: [benchmarks, evaluation, coding-agents, loop-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2608.00267'
    hash: sha256:da50e26db4b6652f26795f68836e4fb8270bec5379729dc7b256336acbb4f230
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A long-horizon coding benchmark of 112 dependency-structured tasks, each a DAG of separately testable development units drawn from pull-request sequences, university course labs and research-paper evolutions, released with its tests, environments and evaluation code."
  url: "https://loopsbench.ai/"
---

LoopsBench is a benchmark for evaluating the loop engineering layer of coding agents over long
horizons. It was introduced in
[[ScholarlyArticle/loopsbench-from-harness-engineering-to-loop-engineering-in-coding-agent-evaluation]].
Each task is a directed acyclic graph whose nodes are source-grounded development units and whose
edges are prerequisite relations, so that intermediate units can be tested separately and a loop's
progress, ordering and preservation of earlier work can be observed rather than only its end state.

## Contents

The benchmark contains 112 tasks — 29 PR Sequences, 57 Course Labs and 26 Research Evolutions —
spanning 9 domains and 8 programming languages, with a median dependency depth of 6 and more than
5,300 development units. A development unit carries a requirement, a file or symbol scope, a set of
prerequisite units, a reference patch contribution and its own tests. Each task is a self-contained
directory with a Dockerfile (and a docker-compose file for multi-service tasks), a test entry point
script, the reference solution, task metadata including the DAG topology, per-unit requirement files
and per-unit test directories, and the base codebase the solution applies to. The evaluated loop sees
the global instruction, unit manifests and attached tests, while the reference patches, the active
ready frontier and scoring state remain evaluator-only.

The accompanying runtime releases a unit's tests only when all of its prerequisites pass, keeps
completed units' tests enforced as regression obligations, samples the workspace from a separate
container on a fixed cadence, and records a loop trace from which metrics such as resolve rate, test
pass rate, dependency depth, regression rate and planning fidelity against the reference DAG are
computed. Any valid topological execution order is accepted.

## Provenance

Source artifacts came from three kinds of public material: university programming projects collected
from the official course pages of 30 universities and public mirrors of their assignment releases;
the commit history and merged pull requests of 56 actively maintained GitHub repositories; and 212
highly cited papers with open-source official implementations, together with their cited prior work
and forward citers. Candidates were normalized into tasks (partly with Claude Code-based extraction
and classification steps) and kept only if they spanned at least 2.5 months and met a minimum
solution scale. Dependency edges were admitted only on unambiguous evidence — overlapping hunks in the
same file, or an import, call or subclass of a definition introduced by an earlier unit — with a
denylist against spurious chains from frequently touched files and generated artifacts. Task
instructions were produced from the gold diff by a Claude Code-based step backed by Claude Opus 4.7
that states the acceptance contract while hiding the implementation path and stripping repository
names, course identifiers, paper titles and author attributions; unit tests were admitted only after
checks for solvability, non-triviality and discriminativeness. The authors state that they release
all tasks, development units and executable tests, with the code at microsoft/Loopsbench.

## Use

The introducing paper evaluates frontier models and six loop implementations on the benchmark and
reports a best resolve rate of 25.00%; its findings are summarized on the paper's page.
