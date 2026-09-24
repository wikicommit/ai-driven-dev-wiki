---
title: "RepoComplianceBench"
type: "schema:Dataset"
lang: en
tags: [benchmark, open-source, ai-governance, coding-agents]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.26819'
    hash: sha256:1eacfc0f1ecc9c6417e146a4780acd58380742a08adb36aaed687c0c20270840
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A benchmark of 106 issue instances from 49 open-source repositories that tests whether a coding agent discovers and follows the repository's written AI contribution rules — refusal, disclosure, verification or handoff — while resolving an ordinary issue."
---

RepoComplianceBench is a benchmark of 106 issue instances drawn from 49 open-source repositories,
each testing whether a coding agent adheres to one of four types of AI contribution rule: refusal of
banned contributions, disclosure of AI assistance, verification of submitted work, and handoff of
critical steps to a human. It was introduced in
[[ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities]].
Unlike benchmarks that hand the agent the rule it is to obey, it leaves the rule in the repository's
own governance files, where the agent has to find it, and it treats compliance rather than repair
quality as the measured outcome.

## Contents

Each instance pairs an ordinary issue with a sanitised snapshot of the repository at its pre-fix
state, including the repository's contributing rules, and names one focal policy provision under
test. The deliverable an agent produces mirrors a real contribution: commits plus a pull-request
description, pre-seeded from the repository's pull-request template. The rule can reach the agent
through three channels — the PR template, `AGENTS.md`, and `CONTRIBUTING.md`. Nineteen instances
already carry their focal clause in a file the harness loads automatically and serve as a control
stratum. The frozen run set samples every Handoff-eligible instance and 30–31 per remaining rule,
with at most two instances per repository and rule, giving 280 runs per agent.

## Provenance

The benchmark grew from a corpus of 455 AI-related norms hand-coded from the written policies of 102
open-source communities. The 88 GitHub repositories among them formed the eligible population; each
received a policy card splitting every AI-relevant passage into single-label provisions (Refuse,
Disclose, Verify, Handoff or residual), each carrying its verbatim source text and location.
Instances were selected by a frozen, rule-based protocol: issues closed within 180 days before a
fixed cutoff, mechanical hygiene gates over 16.2k scanned issues, screening by an LLM curator blind
to the fix, and a temporal gate requiring the focal provision's exact text to exist at the pre-fix
base commit; 257 instances across 58 repositories passed. Workspaces are rebuilt from an empty
repository by fetching only the base commit and its ancestry, so the fix never enters the object
store and no remote is configured, and a validator checked all 257. The benchmark reuses
[[Dataset/swe-bench]]'s issue-to-patch substrate and contamination discipline.

## Use

Compliance is judged in two stages: a mechanical pass marks technical failures and voids any run
that reaches the solution, and an evidence-bound LLM judge, guided by human-written per-rule rubrics
and calibrated on a sample labelled by two authors, decides the rest; partial satisfaction,
uncertain answers and unresolved citations count as non-compliance.
[[ScholarlyArticle/a-first-look-at-coding-agents-compliance-with-ai-contribution-rules-in-open-source-communities]]
used it to evaluate four agent–model pairs and found that agents opened the focal policy file in
3.5% of unaided runs and that refusal and handoff stayed at 0% for every agent unaided.
