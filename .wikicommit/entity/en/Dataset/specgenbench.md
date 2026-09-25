---
title: "SpecGenBench"
type: "schema:Dataset"
lang: en
tags: [formal-specification, program-verification, benchmark]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2401.08807'
    hash: sha256:6a6004213a4b820907bab2aba7366b089e0ffbc10ea7d98d01378dd2d970b075
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A dataset of 120 Java programs with hand-written, verifiable JML specifications, assembled by the SpecGen authors to evaluate formal program specification generation on a wider range of control-flow structures than the SV-COMP Java benchmark."
---

SpecGenBench is a dataset of 120 Java programs with ground-truth formal specifications written by experts, built by the authors of [[ScholarlyArticle/specgen-automated-generation-of-formal-program-specifications-via-large-language-models]] to evaluate automated specification generation. They present it as a contribution intended to facilitate follow-up research.

## Contents

The programs involve a variety of control-flow structures and data structures, such as arrays and strings, and their specifications include post-conditions and loop invariants with both linear and nonlinear relationships between variables. The programs fall into five categories by control-flow structure: Sequential (26 programs, no branches or loops), Branched (23, loop-free with branches), Single-path Loop (24, one loop layer without branches in the body), Multi-path Loop (26, branches in the loop body) and Nested Loop (21). The programs average 20.77 lines of code and a cyclomatic complexity of 6.60.

## Provenance

The authors built SpecGenBench because the SV-COMP Java benchmark they also used is dominated by loop-free programs (88.7% by their analysis), and because few datasets exist specifically for specification generation. Twenty programs, with their specifications, come from a dataset constructed by Nilizadeh et al., and 100 come from LeetCode. The selected programs were confirmed to have behaviour expressible as verifiable JML specifications. For the LeetCode programs, three experts in formal verification wrote specifications that had to pass the verifier, following Nilizadeh et al.'s procedure; where several experts produced verifiable specifications for a program, another expert chose one as the ground truth.

## Use

In the SpecGen paper, SpecGen handled 100 of the 120 SpecGenBench programs, against 91 for AutoSpec, and was the only approach reported to handle seven programs that the baselines could not, five of them in the Nested Loop category. The paper also uses the dataset to measure verifier-call efficiency and draws the 15 programs for its user study from it.
