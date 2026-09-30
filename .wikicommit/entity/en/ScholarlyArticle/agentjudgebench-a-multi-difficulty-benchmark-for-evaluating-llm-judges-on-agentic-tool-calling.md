---
title: "AgentJudgeBench: A Multi-Difficulty Benchmark for Evaluating LLM Judges on Agentic Tool-Calling"
type: "schema:ScholarlyArticle"
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
  description: "A ServiceNow AI paper that introduces the AgentJudgeBench benchmark and uses it to measure how reliably LLM judges score multi-step, dependency-structured tool-calling plans against a deterministic programmatic reference, with and without the ground-truth trace."
  author: ["Abhigya Verma", "Amit Kumar Saha", "Seganrasan Subramanian", "Sai Harshitha Aluru"]
  abstract: "LLM judges are widely used to evaluate agentic tool-calling systems, yet their reliability on structured, dependency-driven workflows remains largely unexamined. The paper presents AgentJudgeBench, 3,808 instances spanning six DAG topologies and three difficulty tiers, evaluated with five generators and six judges under paired with- and without-ground-truth conditions. Judge alignment degrades monotonically with task difficulty, faster without ground truth; on hard queries without ground truth all six judges converge to a 77–82% band; ground-truth exposure reduces alignment for GPT-5.4 and Gemini-2.5-Pro; chain-of-thought and judge temperature have negligible effect, while structured rubrics improve alignment by up to 6.5 pp but do not generalise uniformly."
  keywords: ["LLM-as-a-judge", "agentic tool-calling", "benchmark", "judge reliability", "ground truth"]
---

This paper examines a practice that evaluations of tool-using agents increasingly rely on: using an
[[DefinedTerm/llm-as-a-judge]] to score an agent's tool calls. The authors argue that judge
reliability is well characterised for text tasks such as dialogue and summarisation, but that
tool-calling differs, because correctness there means choosing the right tools from a typed schema,
supplying well-formed arguments, ordering calls to respect execution dependencies and covering the
whole request — four aspects that can fail independently — and because in deployment a judge usually
has no ground-truth execution trace to compare against. Existing benchmarks that use LLM judges for
tool-calling, they note, report only an aggregate agreement figure.

To measure this, the paper introduces [[Dataset/agentjudgebench]]: synthetic records in the format
of the [[Dataset/berkeley-function-calling-leaderboard]], extended to multi-step workflows whose
tool calls form a directed acyclic graph, each with a programmatically verified ground-truth trace.
Five generator models — four open-weight models from 3B to 70B parameters and GPT-5.4 — produce
tool-call plans, which a deterministic programmatic judge and six LLM judges (GPT-5.4, Claude Sonnet
4.5, Gemini-2.5-Pro, QwQ-32B, GPT-OSS-20B and GPT-OSS-120B) each score on tool selection, parameter
structure, sequence accuracy and query coverage. Every LLM judge scores every output twice, once
shown the ground-truth tool calls and once without them, and its alignment with the programmatic
reference is measured across 321,648 paired evaluations. The authors describe their contribution as
this reliability protocol rather than any one of its components, each of which has prior work.

## Key Points

- Judge alignment with the programmatic reference falls monotonically from easy to hard queries for
  all 30 generator–judge pairs, and roughly 1.5 times faster without ground truth than with it.
- On hard queries without ground truth, all six judges converge to a 77–82% band for four of the
  five generators, including GPT-5.4, which the authors read as a task-level rather than judge-level
  ceiling. A recalibrated prompt that defaults to 0.5 instead of 1.0 moved it by at most 1.0
  percentage point for the three strongest generators but by 4.1–5.6 points for the two weakest, so
  the ceiling is partly prompt-dependent for weaker generators.
- Showing the judge the ground truth is not uniformly helpful: it raised alignment for QwQ-32B and
  GPT-OSS-120B but lowered it for GPT-5.4 (by 1.5 points) and Gemini-2.5-Pro (by 3.9 points). The
  authors attribute this to over-anchoring on the reference's ordering, and a control in which the
  reference was replaced with one from a different record left Gemini-2.5-Pro's alignment
  essentially unchanged.
- Chain-of-thought in the QwQ-32B judge changed alignment by at most 0.3 points in any cell, and
  judge temperature by at most 0.6 points. A structured per-metric rubric beat a free-form prompt by
  4.8–6.5 points on one judge–generator pairing, but on a second pairing the gain was smaller and
  reversed on hard queries, so the authors treat prompt format as real but pairing-dependent.
- Inter-judge agreement was moderate (mean Cohen's κ about 0.42 with ground truth), and a soft jury
  of all six judges matched but did not exceed the best individual judge.
- Which judge is best depends on the setting: with ground truth, QwQ-32B agrees most closely with the
  programmatic reference; without it, GPT-5.4 and Gemini-2.5-Pro lead by at most about one point. In
  a 120-record single-annotator human study, GPT-OSS-120B was the judge closest to human verdicts,
  while QwQ-32B fell to fourth.
- A judge-specialised model, Prometheus-2, added as a baseline, aligned 20–30 points lower than the
  six general-purpose judges and agreed with them at close to chance level.

## Notes

The programmatic scorer serves as the reference because only a deterministic scorer scales to the
full evaluation grid without reintroducing the reliability question under study. The human study
agreed with it on 92.7% of metric-level verdicts overall but only 82.5% on parameter structure,
where the scorer penalises extra argument keys that are valid under the tool schema; the authors
report that correcting for this would move each judge's alignment by at most 0.09 points without
changing the ranking.

Stated limitations include the synthetic rather than real-trace data, which leaves domain drift as an
open concern; the medium difficulty tier, whose rewrites were unanimously judged harder than the
easy ones for only 58.1% of sampled records and so should be read as a robustness check; the use of
GPT-5.4, a non-reproducible Azure snapshot, as generator, judge and rewrite meta-judge; and the
restriction to evaluation-time reliability. The authors flag, as untested future work, that the
without-ground-truth ceiling would be a higher-risk failure if such a judge were used as a reward
signal for training a tool-calling agent. They offer a deployment guide recommending judges per
scenario and advise against relying on any single judge, complementing LLM judges with programmatic
scoring and human review.
