---
title: "The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, tool-use, survey]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2603.22862'
    hash: sha256:d90cb0534d8f41e8417040b9c8b95eb7d8b673455e2d229599a7923fd198bd96
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A survey of multi-tool LLM agents that treats long-horizon orchestration of many tools, rather than a single correct tool call, as the central problem, and organizes the literature along six connected dimensions from inference-time planning to benchmark design."
  author: ["Haoyuan Xu", "Chang Li", "Xinyan Ma", "Xianhao Ou", "Zihan Zhang", "Tao He", "Xiangyu Liu", "Zixiang Wang", "Jiafeng Liang", "Zheng Chu", "Runxuan Liu", "Rongchuan Mu", "Dandan Tu", "Ming Liu", "Bing Qin"]
  abstract: "The survey observes that research on tool use in large language models has moved from whether a model can select and execute a correct single tool call to multi-tool orchestration over long trajectories with intermediate state, execution feedback, changing environments and constraints on safety, cost and verifiability. It unifies task formulations, organizes the literature around six core dimensions, summarizes applications in software engineering, enterprise workflows, graphical user interfaces and mobile systems, and outlines future directions for reliable, scalable and verifiable multi-tool agents."
  keywords: ["tool use", "multi-tool orchestration", "LLM agents", "survey"]
---

This survey, led by researchers at Harbin Institute of Technology, reviews
[[DefinedTerm/agentic-tool-use]] from the point at which a single correct call stops being the
interesting question. Early tool-learning work, including [[DefinedTerm/react-prompting]], taught
models to recognize an intent and format an API request; the authors argue that practical agents now
have to coordinate many tools over long trajectories, preserve intermediate state, recover from
failures and operate under limits on latency, cost and safety, so that the core difficulty has become
orchestration rather than access. They frame this as a qualitative change in the decision space —
from choosing a tool to a series of coupled decisions covering tool-subset selection, cross-tool
dependencies, sequential and parallel scheduling, failure recovery and re-planning.

The survey is motivated by two gaps the authors see in the literature. One is conceptual: terms such
as tool use, tool calling, tool retrieval, workflow execution and orchestration are used loosely even
though they denote different capability levels. The other is structural: planning, training, safety,
efficiency, benchmarking and open-environment adaptation are usually studied separately, while
deployed agent systems depend on how they interact. It therefore first gives a unified formulation of
multi-tool orchestration — a policy choosing tool calls or termination from the interaction history
and memory, under a cost-aware objective that trades task success against calls, latency, fees and
risk — and then organizes the field around six connected dimensions.

## Key Points

- The six dimensions are inference-time planning and execution, training and trajectory
  construction, safety and control, efficiency under resource constraints, capability completeness in
  open environments, and benchmark design and evaluation.
- On inference, the authors describe a shift from linear, ReAct-style sequential traces to
  topology-aware planning over graphs and hierarchical decompositions, and from "generate once and
  execute" to "search, verify, and then commit"; long-horizon orchestration additionally relies on
  division of labour between components, routing across large tool ecosystems, and memory that
  compresses or externalizes execution history.
- Tuning methods are arranged in ascending order of compute and data dependency — training-free
  methods (tool retrieval, prompting, non-parametric memory), multi-tool trajectory synthesis,
  supervised fine-tuning and reinforcement learning — and the authors argue that for synthetic data
  the critical measure is now coverage of long-tail and multi-step error patterns rather than
  quantity.
- They split multi-tool safety risks into two dimensions: parallel execution, where concurrent write
  operations risk race conditions and inconsistent state, and long-horizon tool chains, where
  malicious content or small upstream errors propagate and amplify across steps. Defences are
  described as moving from pre-execution constraints through transaction-style isolation and
  rollback to post-execution verification.
- Efficiency work is grouped into reducing latency (parallel execution, asynchronous decoupling of
  planning from acting, speculative execution) and reducing cost (dynamic tool retrieval instead of
  placing every tool description in the prompt, adaptive model routing, caching and memory).
- Capability completeness is described as a loop of perceiving capability boundaries (clarifying or
  terminating instead of hallucinating tools), autonomous [[DefinedTerm/tool-creation]], and
  open-environment adaptation through reusable experience and skill memory.
- Benchmarks are traced from single-point call correctness to four dimensions of long-horizon
  capability — topological complexity of tool dependencies, temporal scale, dynamic environments, and
  state persistence with self-correction — and the authors argue that long-horizon evaluation should
  not rely solely on endpoint success.
- For applications, the authors argue that differences between domains stem mainly from their
  operational bottlenecks rather than from orchestration topology — for software engineering, success
  grounded in deterministic tests and the cost of test verification; for enterprise workflows,
  transactional consistency, auditing and permission boundaries.

## Notes

The survey positions itself against earlier surveys of tool learning and LLM agents by taking
multi-tool orchestration, rather than tool use in general or agent systems broadly, as its unit of
analysis, and by drawing boundaries between concepts it considers often conflated — tool invocation,
tool retrieval, orchestration and toolset expansion. Its closing agenda asks for better abstractions
for stateful orchestration, stronger evaluation protocols for dynamic and long-horizon settings, and
closer integration of model-level reasoning with system-level guarantees; for applications it lists
adaptive regression against interface drift, process-level verifiability and replayable audits, joint
optimization of cost, latency and quality, and composable, adversarially robust failure recovery.

The version extracted here is arXiv:2603.22862v2 [cs.SE], formatted with an ACM template whose venue
fields are still placeholders and a stated publication date of April 2026. The authors are
affiliated with Harbin Institute of Technology, Harvard University and Huawei Technologies.
