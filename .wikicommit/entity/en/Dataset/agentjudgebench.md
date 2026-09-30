---
title: "AgentJudgeBench"
type: "schema:Dataset"
lang: en
tags: [llm-as-a-judge, tool-use, benchmarks, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2608.26623'
    hash: sha256:32ddb06e75bc0c6262a2919dd3df52b1d322485af3eb3da7457c44270979c3ba
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A benchmark of 3,808 synthetic, multi-step tool-calling records with programmatically verified ground-truth traces, spanning six dependency-graph topologies and three difficulty tiers, built to measure how reliably LLM judges score agentic tool-calling."
  creator: ["ServiceNow AI"]
  url: "https://huggingface.co/datasets/ServiceNow-AI/AgentJudgeBench"
  variableMeasured: ["tool selection accuracy", "parameter structure accuracy", "sequence accuracy", "query coverage accuracy"]
---

AgentJudgeBench is a benchmark for evaluating LLM judges — not agents — on agentic tool-calling. Each
record pairs a user request and a typed tool inventory with a ground-truth sequence of tool calls
whose execution dependencies form a directed acyclic graph, so that a judge's verdict on a
generated plan can be compared with a deterministic programmatic score. It was built by ServiceNow
AI and introduced in
[[ScholarlyArticle/agentjudgebench-a-multi-difficulty-benchmark-for-evaluating-llm-judges-on-agentic-tool-calling]].

## Contents

The benchmark has 3,808 records across 15 enterprise domains, such as IT service management, contract
lifecycle management and energy grid operations. Each record follows the format of the
[[Dataset/berkeley-function-calling-leaderboard]], extended from single-turn calls to multi-step
workflows, and belongs to one of six topologies: linear, fan-out, fan-in, diamond, optional
enrichment and loop-like. The distribution is deliberately uneven — fan-in is the most common at
27.5% and loop-like the rarest at 5.9% — which the authors say mirrors how often each pattern occurs
in enterprise agentic workloads. A record exposes 8–19 available tools (mean 12.9), of which the
ground-truth trace calls 2–5 (mean 3.3), so the model has to select tools rather than use all of
them.

Each record is rewritten into easy, medium and hard variants by increasing the ambiguity of the query
while holding the task and ground-truth trace fixed, giving 11,424 rows. The released data also
contains the outputs of five generator models and the verdicts of seven LLM judges, scored on four
metrics — tool selection, parameter structure, sequence accuracy and query coverage — with and
without the ground truth shown to the judge.

## Provenance

The records are generated synthetically on SyGra, an open-source graph-oriented synthetic data
framework: from an enterprise domain label, a pipeline produces use-case scenarios, a typed tool
inventory, executable pseudocode linking the tool dependencies, a natural-language request and the
ordered execution trace. The authors chose synthetic generation because a controlled reliability
study needs a trace certified as correct for every record, systematic coverage of topologies and
difficulty tiers, and domain diversity, which they say real enterprise traces rarely provide.

Every trace passes a two-level quality gate with no LLM involved — JSON-schema validation, argument
type checking and trace consistency checks, followed by programmatic checks of each request–tool-call
pair — and failing records are regenerated. A check by three LLM meta-judges found the medium→hard
rewrite unanimously judged harder for 93.9% of sampled records but the easy→medium rewrite for only
58.1%, so the authors treat the medium tier as a robustness check rather than a calibrated midpoint.
The dataset is published at <https://huggingface.co/datasets/ServiceNow-AI/AgentJudgeBench>, and the
pipeline code in the SyGra repository.

## Use

[[ScholarlyArticle/agentjudgebench-a-multi-difficulty-benchmark-for-evaluating-llm-judges-on-agentic-tool-calling]]
uses the benchmark to compare six general-purpose LLM judges and one judge-specialised model across
five generators, finding that judge alignment falls with query difficulty, that without ground truth
all six general-purpose judges converge to a 77–82% band on hard queries for four of the five
generators, and that exposing the
ground truth lowers alignment for some frontier judges.
