---
title: "DocsChisel: Adaptive Tool Documentation Optimization Framework for LLM Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [tool-use, agents, documentation, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2608.10037'
    hash: sha256:fbaa95d6d1522f017711102c2448649915aaaa63d497d75c53679ee043b611f6
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Fudan University study of how the information fields in tool documentation affect LLM agents, which proposes DocsChisel, a framework that rewrites each tool's documentation at the field level from a target agent's failed execution traces."
  author: ["You Lu", "Kun Zhang", "Bihuan Chen", "Xin Peng"]
  abstract: "Existing studies mainly improve the tool-use capabilities of LLM agents while treating tool documentation as a fixed input. A large-scale empirical study of tool documentation finds substantial heterogeneity in the information fields it provides, and that the effectiveness of different fields depends on task domain, LLM backbone and agent paradigm, so no fixed documentation generalises across agent settings. DocsChisel analyses failed execution traces of a target agent to identify documentation-related issues and iteratively optimises each tool's documentation by adding, removing and refining information fields. Against EASYTOOL and DRAFT, it improves agent task success rate by 95.89% over the original documentation and by 75.15% on average over the baselines, with limited optimisation time and token overhead."
  keywords: ["tool documentation", "LLM agents", "documentation optimization", "information fields", "tool use"]
---

This paper, by four authors at Fudan University, treats tool documentation as a grounding resource
for LLM agents rather than a fixed input. It observes that documentation written for agents differs
from traditional API documentation in both audience and content: the reader is an agent that must
infer a tool's function and produce executable invocations directly from in-context text, so the
emphasis shifts to usage conditions, parameter semantics, invocation constraints and output
interpretation. Earlier documentation optimisers, it argues, mostly rewrite, correct, standardise or
compress within the fields a document already has, and pay less attention to whether those fields
are sufficient, redundant or suited to a particular agent.

The paper first reports an empirical study. It collected documentation for 24,955 tools from 14
tool-use datasets and aligned their contents into 17 information fields, then measured on WorkBench
how adding or removing one field at a time changed task success rate under two agent paradigms — a
ReAct agent built with LangChain and a multi-agent system built with AutoGen — and three backbones
(GPT-4o, GLM-5 and Claude Haiku 4.5). It then proposes DocsChisel, which groups tools and queries by
task domain, runs the target agent to collect failed traces, and for each tool iterates three
LLM-assisted steps — diagnosing failed traces, planning field-level add, remove or refine
operations, and generating new documentation anchored to the original — with domain-level memories
of failure patterns, operations and edits carried between iterations. A candidate is kept only if
it does not lower validation task success, and the best candidate after the iteration budget
(five by default) is selected, ties going to the shortest.

## Key Points

- Across the 14 datasets, only tool name and functionality description appeared in all of them;
  usage guidance and invocation constraint appeared in only two.
- The same field could have different or opposite effects in different settings: with GPT-4o and
  ReAct only 6 of the 17 fields had the same direction of effect across three task domains, 12 of
  17 changed direction across the three backbones, and switching from ReAct to multi-agent reversed
  the effect of several fields. Adding or removing a single field changed task success rate by 6.34
  percentage points on average. The authors conclude that no fixed documentation convention
  generalises across agent settings.
- Evaluated on 74 tools and 2,072 queries across nine task domains from WorkBench and API-Bank,
  DocsChisel achieved the highest average tool invocation correctness and task success rate in
  every evaluated setting, improving them by 34.69% and 95.89% over the original documentation and
  by 30.83% and 75.15% on average over the EASYTOOL and DRAFT baselines.
- Optimised documentation averaged 189.23 tokens, 24.02% longer than the original and comparable to
  DRAFT's. Optimisation used 6.35% fewer tokens than DRAFT but took 12.65 minutes per tool on
  average, longer than either baseline.
- The optimisation model mattered: with Claude Haiku 4.5 as optimiser, results were better than
  with GLM-5 or GPT-4o. Most of the gain came in early iterations, and disabling the memory
  mechanism left both metrics largely flat after the second iteration, reducing final task success
  by 76.47% relative to the full framework.

## Notes

The authors attribute DocsChisel's advantage to diagnosing failures from complete agent traces and
adapting field composition to the target agent, contrasting it with a fixed-template approach and
with one that refines documentation from isolated tool executions. They note that some failures
come from outside the documentation — task decomposition errors, stochastic reasoning, incomplete
queries — which documentation optimisation cannot remove. Stated threats to validity include the
choice of paradigms, backbones and datasets, and manual steps in identifying fields and building
documentation variants, which they mitigated with independent annotation (Cohen's kappa 0.862);
each setting was run as three optimisations with five evaluations each, and improvements remained
significant under a Mann-Whitney U test with Holm correction. Related wiki coverage of rewriting
tool descriptions for agents includes
[[ScholarlyArticle/learning-to-rewrite-tool-descriptions-for-reliable-llm-agent-tool-use]].
