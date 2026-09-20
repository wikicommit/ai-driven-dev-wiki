---
title: "Advances and Frontiers of LLM-based Issue Resolution in Software Engineering: A Comprehensive Survey"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, surveys, software-maintenance, reinforcement-learning]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2601.11655'
    hash: sha256:cbedafca04b35cddb49e45fd2b158a2fc521a51a9ea5da37f4059553ec41b806
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A survey of LLM-based issue resolution organised around a three-part taxonomy of data, methods and analysis, synthesising 175 papers and online resources. It covers dataset construction, training-free and training-based methods, and empirical critiques of benchmark quality and agent behaviour."
  author: ["Caihua Li", "Lianghong Guo", "Yanlin Wang", "Daya Guo", "Wei Tao", "Zhenyu Shan", "Mingwei Liu", "Jiachi Chen", "Haoyu Song", "Duyu Tang", "Hongyu Zhang", "Zibin Zheng"]
  datePublished: "2026-01-15"
  abstract: "The survey presents issue resolution as a Software Engineering task integral to real-world development that has become a compelling challenge for artificial intelligence, and credits the establishment of benchmarks like SWE-bench with revealing the task as profoundly difficult for large language models and thereby accelerating the evolution of autonomous coding agents. It examines data construction pipelines covering automated collection and synthesis approaches, analyses methodologies spanning training-free frameworks with their modular components and training-based techniques including supervised fine-tuning and reinforcement learning, discusses critical analyses of data quality and agent behaviour alongside practical applications, and identifies key challenges and future directions."
---

This survey maps the field of LLM-based issue resolution, the task of taking an issue description and
a repository and producing a patch that resolves it. Its authors describe it as the first survey
dedicated to this domain, written against a literature they characterise as fragmented — existing
surveys, they argue, focus on code generation and do not address the harder problem of issue
resolution. The corpus is 175 publicly available papers and online resources, gathered by citation
tracking and snowballing, and organised under a taxonomy with three top-level dimensions: **data**,
**methods** and **analysis**.

The paper formalises the task before surveying it. An instance is written as `I = (D, C, T)`,
comprising an issue description `D`, a codebase `C` and corresponding tests `T`; only `D` and `C` are
observable during resolution, alongside an environment `E` that can be explored. A method `M` is
expected to produce a patch `P = M(D, C, E)`, which is applied to the codebase and evaluated by
running `T` against the modified result. The aggregate metric is the **Resolved Rate**, the mean
of the per-instance binary outcomes over a dataset.

The methods half of the taxonomy separates training-free from training-based work. Training-free
methods are grouped by framework (single-agent, multi-agent and fixed-workflow designs), by
plug-and-play module (tools for repository interaction, memory for experience accumulation) and by
inference-time scaling. Training-based methods split into supervised fine-tuning and reinforcement
learning. The analysis half surveys empirical critiques of the field's own evidence base — studies of
benchmark data quality and of agent behavioural pathology — rather than new techniques.

## Key Points

- The survey frames SWE-bench as marking a departure from earlier work on software *generation*, such
  as ChatDev and MetaGPT, toward the later lifecycle stages of software maintenance and evolution,
  and describes it as catalysing a research frontier focused on navigating and modifying
  environments.
- It classifies training-free methods into three categories based on the underlying framework:
  frameworks (high-level architectures — single-agent, multi-agent, fixed-workflow), modules
  (plug-and-play augmentations such as tools and memory), and inference-time scaling, which uses
  search or parallelisation to raise success rates without modifying model parameters.
- Tool modules are organised along a standard repair pipeline — bug reproduction, fault localisation,
  code search, patch generation, patch validation and test generation — and the survey notes that
  fault localisation approaches include method-level spectrum-based fault localisation and
  graph-based methods that construct code dependency graphs to trace fault propagation.
- On memory, it reports a shift in the field's frontier from storing raw data toward abstracting
  high-level policies from both successful and failed trajectories, and describes dual-process
  cognitive architectures that pair episodic records of concrete repairs with semantic layers of
  abstract insight to support retrieval conditioned on current context.
- For supervised fine-tuning it identifies three recurring dimensions: data scaling through
  synthesised corpora, multi-stage curriculum learning that progresses from broad trajectory
  ingestion to strictly filtered subsets or specialised tasks, and rejection sampling pipelines that
  fine-tune only on successful trajectories while training verifiers to re-rank solutions at
  inference time.
- For reinforcement learning it decomposes the problem into algorithm, reward design and scaffold,
  naming Group Relative Policy Optimization as the dominant algorithmic choice for avoiding the
  computational burden of a critic model, with Proximal Policy Optimization and Direct Preference
  Optimization used in narrower settings.
- It reports from its own statistics that OpenHands is the most prevalent scaffold used for
  reinforcement-learning rollouts, followed by workflow-based methods (notably Agentless and
  two-stage workflows), with environment-native frameworks such as R2E-Gym and SWE-Gym also
  frequently adopted because they align with training data.
- Its data analysis section reports that agent success rates are frequently inflated by solution
  leakage, ambiguous issue descriptions and weak test suites that fail to catch incorrect patches,
  and that because manual cleanup is too costly and inconsistent at scale, the field is shifting
  toward automated validation workflows using model-based consensus to distinguish valid fixes from
  false positives.
- Its methods analysis reports a behavioural failure mode in which models prioritise prolonged
  internal deliberation over necessary environmental interaction, which the cited work characterises
  as leading to analysis paralysis and rogue actions.
- Among its challenges it argues that current evaluation focuses on effectiveness metrics such as
  resolve rates while overlooking efficiency metrics such as API costs and inference time, creating a
  bias in which the computational and economic burdens of high-performing models are obscured.
- It identifies the reliance on outcome-level rewards — typically a binary test pass/fail signal — as
  a limitation for a task that requires multi-turn interaction, because an outcome reward makes
  credit assignment across action steps ambiguous, and proposes finer-grained process rewards as a
  direction.
- It names data leakage and contamination as a threat to evaluation reliability as benchmarks
  approach saturation, noting that unclear training cutoff dates may let models memorise solutions
  while the benchmarks themselves carry invalid instances including ambiguous descriptions, solution
  hints and insufficient test coverage.
- It reports that current research predominantly addresses the implementation and integration phases
  of the software development lifecycle, and argues the scope should broaden to other stages such as
  requirements analysis and architectural design.

## Notes

The authors maintain an open-source repository tracking datasets, implementations and new
developments in the field, which they describe as a dynamic resource intended to be updated
continuously.

The paper's Limitations section states that, as the first dedicated survey on issue resolution, it
prioritises high-level summaries over exhaustive detail because of space constraints, and that its
search methodology relied on citation tracking and snowballing — thorough, in the authors' account,
but liable to overlook niche or nascent works.

It relates to several neighbouring subjects this wiki already covers.
[[DefinedTerm/software-issue-resolution]] is the task the survey is about;
[[DefinedTerm/agentless]] and [[SoftwareApplication/openhands]] are among the scaffolds whose
prevalence it quantifies.
