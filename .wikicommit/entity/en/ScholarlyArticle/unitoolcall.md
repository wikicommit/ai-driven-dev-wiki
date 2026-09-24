---
title: "UniToolCall: Unifying Tool-Use Representation, Data, and Evaluation for LLM Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, tool-use, evaluation, benchmarks, fine-tuning]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.11557'
    hash: sha256:ab37d3f05bacb9267936f2f0275dbd927ce5620a5b0d81a15ecd5b75f82e6ba9
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A preprint presenting UniToolCall, a framework that puts tool-use training data and evaluation benchmarks for LLM agents into one shared Query–Action–Observation–Answer (QAOA) representation, together with a 22K-tool pool, a 390K-instance hybrid training corpus and a unified multi-granularity evaluation protocol."
  author: ["Yijuan Liang", "Xinghao Chen", "Yifan Ge", "Ziyi Wu", "Hao Wu", "Changyu Zeng", "Wei Xing", "Xiaoyu Shen"]
  abstract: "The paper argues that research on tool use in LLM agents represents the query-to-answer chain inconsistently, rarely studies serial/parallel and hop/turn effects, and evaluates under incompatible protocols and metrics. UniToolCall standardizes the pipeline from toolset construction and dataset generation to evaluation: it curates a pool of 22k+ tools, builds a 390k+ instance hybrid training corpus from ten standardized public datasets and structurally controlled synthetic trajectories, adds an Anchor Linkage mechanism that enforces cross-turn dependencies, and converts seven public benchmarks into a unified QAOA representation evaluated at the function-call, turn and conversation levels."
  keywords: ["tool learning", "function calling", "synthetic data", "benchmark unification", "multi-turn tool use"]
---

This preprint, by researchers at the Eastern Institute of Technology, Ningbo, the University of
Science and Technology of China and The Hong Kong Polytechnic University, addresses what it calls the
fragmentation problem in tool learning for [[DefinedTerm/agentic-tool-use]]. The authors describe it
along three dimensions: *representation inconsistency* (datasets encode tool calls, arguments and
observations in incompatible schemas, which makes joint training difficult), *structural
incompleteness* (existing pipelines largely overlook the distinction between serial and parallel tool
invocation), and *evaluation mismatch* (benchmarks rely on disparate protocols, tool definitions and
scripts, which prevents fair cross-dataset comparison).

UniToolCall responds by standardizing the whole pipeline under one Query–Action–Observation–Answer
(QAOA) representation. It first assembles a tool pool from academic benchmarks, from Model Context
Protocol servers (the top 40 listed on mcp.so at collection time plus 11 used in MCP-Universe) and
from the tool definitions of the paper's own datasets, normalizes every tool into a JSON Schema
format, and filters the pool through exact deduplication, removal of tools whose schemas depend on
temporal attributes, schema validation and embedding-based semantic deduplication, leaving 22,606
tools organized into six functional categories and thirteen application domains. On this pool it
builds a training corpus of 390,060 instances: 387,123 conversations retained from ten standardized
public datasets, plus 2,937 synthetic trajectories generated and self-evaluated by Qwen3-32B, split
evenly across single-hop, multi-hop and multi-turn scenarios with explicit control over serial versus
parallel execution. Synthetic trajectories are assembled with a "Hybrid-20" candidate list — the
ground-truth tools, hard negatives retrieved by embedding similarity, and five random easy negatives,
twenty candidates in all — and the main evaluation uses the same setting.

For evaluation, seven public benchmarks are converted into QAOA, yielding 6,163 conversations, and
scored at the function-call, turn and conversation levels with four metrics: Strict and Flexible
Precision for tool selection, and Strict and Flexible Parameter Accuracy for arguments. A predicted
call is matched first by rule-based exact matching after deterministic normalization, then by
ROUGE-L similarity with a 0.7 threshold. The main model is Qwen3-8B fine-tuned with LoRA, compared
against GPT-5.2 Instant, Gemini 3 Flash Preview, Claude 4.6 Sonnet, Kimi-K2-Instruct, DeepSeek-V3.2
and Qwen3-32B.

## Key Points

- The paper proposes Anchor Linkage, a constraint for synthesizing multi-turn data that requires each
  user query from turn 2 onward to explicitly inherit concrete state — such as transaction IDs,
  coordinates or returned parameter values — from the previous turn. It combines prompting that
  escalates from soft hints to hard inclusion constraints on retries, a regex-based check with a
  fallback that prepends the anchor to the query, and a final gate on an LLM-scored anchor rubric.
- The authors report that without such a constraint, generators produce turns that are locally fluent
  but disconnected from one another, a failure that generic quality scores do not penalize: in a
  comparison of 10 multi-turn trajectories with and without the constraint, clarity, naturalness and
  success scores moved only between −0.25 and +0.21, while the anchor score dropped by 0.85.
- Under the Hybrid-20 setting, the fine-tuned Qwen3-8B reached 92.9% single-hop and 93.0% single-turn
  Strict Precision, the best strict tool-selection scores among the models compared. In multi-hop settings it
  was second-best on Strict and Flexible Precision (80.7% and 89.6%), and Claude 4.6 Sonnet remained
  ahead of it on multi-hop parameter accuracy.
- Strict multi-turn success remains unsolved: almost every model, including the fine-tuned one, scored
  0.0% on conversation-level multi-turn Strict Precision, because one incorrect call zeroes a whole
  episode. On 30 BFCL v3 multi-turn conversations, the share of dialogues still fully correct at turn 2
  was 3.3% for vanilla Qwen3-8B and 50.0% for the fine-tuned model, which also eliminated format and
  parse failures as a first error (30.0% to 0.0%).
- Public tool-use corpora are skewed toward parallel, independent calls: the public subset's
  serial-to-parallel ratio for multi-hop data was 1:5.7 against 1:1.9 in the synthetic data, and the
  filtered BFCL v3 multi-hop split held 141 parallel but only 3 purely serial instances. The authors
  read synthetic data as a complement for sequential structure rather than a substitute for the scale
  and domain coverage of public data.
- Training on a single synthetic structure mainly helps that structure, while a mixed synthetic
  curriculum gave more even generalization than any homogeneous subset.
- Under a matched 20K-instance budget, the recipe improved single-hop and single-turn Strict Precision
  across Qwen3 models from 0.6B to 14B and on two non-Qwen backbones (Gemma-3-4B-it and
  Llama-3.2-3B-Instruct), with gains uneven mainly on multi-hop; a model trained with the test APIs
  removed from its training candidates scored the same multi-hop Strict Precision (22.4%) as one
  exposed to them.

## Notes

The paper compares itself with ToolACE, ToolMind, ToolFlow and TRAJECT-Bench, arguing that none of
those converts heterogeneous public resources into a shared representation with a common
multi-granularity metric suite, while acknowledging that TRAJECT-Bench offers trajectory-level
diagnostics and agentic evaluation that UniToolCall lacks. The benchmarks converted for evaluation
include the [[Dataset/berkeley-function-calling-leaderboard]] (BFCL v3), and the tool pool draws on
[[DefinedTerm/model-context-protocol]] servers.

Limitations the authors state include a maximum context length of 8,192 tokens, which restricts very
long interactions and large tool outputs; scoring by static ground-truth matching, which does not
capture real-time error recovery or policy correction; conversion that may drop features specific to
each native benchmark; and the exclusion of interactive multi-turn parameter filling, in which
missing arguments are elicited through follow-up turns. They plan to extend the framework to dynamic
agent interactions with live tool execution. The version extracted here is arXiv:2604.11557v3.
