---
title: "EvoClaw"
type: "schema:Dataset"
lang: en
tags: [agents, benchmarks]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.05608'
    hash: sha256:0793091fcad2dc48f9eb6412001558cc2e993e5d5904e18d8fd0c943453879be
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A benchmark that evaluates AI agents on continuous software evolution — sustained development across commit histories where each change must preserve system integrity and errors accumulate — rather than on isolated issue fixes."
---

EvoClaw is a benchmark for evaluating AI agents on continuous software evolution. It is described in
[[ScholarlyArticle/agentic-software-restructuring-paradigm]], which describes it as providing the most
sobering data among the challenges that persist for the agentic paradigm it argues for.

## Contents

What distinguishes EvoClaw from isolated-task benchmarks is the shape of the task it poses. Rather than
presenting an agent with a single issue to fix, it requires sustained development across commit
histories, where each change must preserve system integrity and where errors accumulate across the
sequence. That construction is what makes it a test of long-term maintenance and error propagation
rather than of per-task correctness.

## Use

[[ScholarlyArticle/agentic-software-restructuring-paradigm]] reports EvoClaw's headline finding as
overall performance scores dropping significantly from above 80% on isolated tasks to at most 38% in
continuous settings, which that benchmark's authors read as exposing agents' profound struggle with
long-term maintenance and error propagation. The evaluation behind the figure covered twelve frontier
models across four agent frameworks.

The paper reading those results draws four challenges out of them: context drift, as codebases grow
beyond the effective context window and agents lose coherent understanding of system-wide invariants;
error propagation, where a small error in an early commit cascades into compounding failures and agents
lack robust mechanisms for detecting and recovering from those chains; absent technical-debt awareness,
since agents optimise for immediate task completion without modelling the long-term cost of their
design decisions; and verification fidelity, since automated testing remains incomplete and an agent can
pass tests while introducing subtle semantic errors that surface only under novel inputs.

That paper treats the gap between the two figures as quantifying the distance between current agent
capability and the threshold for fully autonomous software engineering — and argues the gap is not
fundamental, reflecting limitations in context management, memory architecture and verification
mechanisms that are active areas of research. It also names long-context state management as one of its
open problems specifically on the strength of this benchmark's result. Note that everything recorded
here about EvoClaw comes from that paper's account of it rather than from the benchmark's own
publication.
