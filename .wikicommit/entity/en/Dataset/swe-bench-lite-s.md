---
title: "SWE-bench Lite-S"
type: "schema:Dataset"
lang: en
tags: [evaluation, coding-agents, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2407.01489'
    hash: sha256:ec78fdd1fa6d6641919d4b68279ff1e8157c8bebd09ad96bd24d862821b708e7
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A filtered version of the SWE-bench Lite benchmark, constructed by the authors of the Agentless paper by excluding problems whose ground truth patch is exact or whose issue descriptions are insufficient or misleading, in order to support a more rigorous evaluation and comparison."
---

SWE-bench Lite-S is a filtered variant of the SWE-bench Lite benchmark, constructed for the purpose
of more rigorous evaluation and comparison of systems that resolve software issues. It is introduced
in [[ScholarlyArticle/agentless-demystifying-llm-based-software-engineering-agents]] alongside the
[[DefinedTerm/agentless]] approach that paper's headline results are measured with.

## Contents

The dataset is SWE-bench Lite with a subset of its problems removed. The authors state the exclusion
criterion in terms of what they found wrong with those problems: issues whose ground truth patch is
exact, and issues whose descriptions are insufficient or misleading.

## Provenance

The filtering is the result of a manual pass over the benchmark rather than an automated one: the
authors of the Agentless paper report that they manually classified the problems in SWE-bench Lite,
and constructed SWE-bench Lite-S by excluding the problematic issues they identified. The stated
motivation is that the original benchmark's defects affect what a comparison between systems
measures, so a filtered version is offered as the basis for that comparison instead.
