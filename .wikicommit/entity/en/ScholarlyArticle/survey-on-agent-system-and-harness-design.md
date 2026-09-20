---
title: "From Question Answering to Task Completion: A Survey on Agent System and Harness Design"
type: "schema:ScholarlyArticle"
lang: en
tags: [agent-architecture, evaluation, benchmarking, context-engineering, survey]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.20683'
    hash: sha256:4d2fd9336c3ac20f51ab2d6d4fc4eb98e0ba0673a8d3475e0e286c3fdfc4511a
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A survey that examines LLM-based agents through a model–harness lens, tracing four paradigms of agent engineering and decomposing the execution harness into six coupled runtime responsibilities. It maps task properties to harness configurations and synthesizes benchmark evidence on how runtime design affects measured performance."
  author: "Jianyuan Guo, Zhiwei Hao, Chengcheng Wang, Cheng Fan, Tingzhang Luo, Hongguang Li, Ying Gao, Hefei Mei, Jiankun Peng, Rongjian Xu, Minjing Dong, Han Wu, Mengyu Zheng, Kai Han, Shiqi Wang, Chang Xu, Yunhe Wang"
  datePublished: "2026-06-14"
  abstract: "LLM-based agents mark a shift from passive question answering to active task completion: they perceive environments, invoke tools, maintain state, and act over extended horizons. As agent systems have evolved from prompt engineering to workflows and context engineering, harness engineering, and agent-native training with co-evolution, a central question has become increasingly important: where does the bottleneck in agent performance reside — in the foundation model, in the execution harness, or in the coupling between them? The survey clarifies the functional definition of agents and the implementation view of an LLM-based agent as a foundation model coupled with an execution harness, analyzes the limits of model-centric scaling, traces four paradigms of agent engineering, and decomposes the execution harness into six coupled runtime responsibilities. Using that decomposition it maps task properties and domain pressures to harness configurations, reviews benchmark and evaluation practices, and synthesizes model–harness evidence on how runtime design affects long-horizon task completion, efficiency and reliability."
  citation:
    - "[[ScholarlyArticle/swe-agent-agent-computer-interfaces-enable-automated-software-engineering]]"
    - "[[ScholarlyArticle/swe-bench-can-language-models-resolve-real-world-github-issues]]"
---

This survey reads the LLM-based agent literature through what its authors call a model–harness lens. It separates two abstraction levels that it says are often conflated: at the functional level an agent is a goal-directed closed-loop system organising five operations around a task objective — perception, state maintenance, reasoning and decision-making, action, and feedback adaptation — while at the implementation level an LLM-based agent is a foundation model coupled with an [[DefinedTerm/execution-harness]]. The model supplies language understanding, reasoning, planning and action proposal; the harness supplies the runtime machinery that exposes observations, constructs context, executes actions, persists state, and verifies or recovers from failures. The survey's central claim is that agent quality — success, efficiency, safety and generalization — emerges from the interaction between model capability, runtime infrastructure, task structure and evaluation design rather than from model capability alone.

Its method is synthesis rather than experiment: it organises published papers, public engineering reports, benchmarks and controlled model–harness comparisons covering LLM-based agent systems from 2020 to 2026. Three claimed distinctions from prior surveys are stated explicitly — that it is evolution-first, organising the literature around engineering paradigm shifts rather than a static component taxonomy; that it is harness-centric, treating the execution harness as a first-class technical object; and that it connects academic evidence with industrial practice. The empirical sections compile leaderboard and public submission data for SWE-bench Verified, Terminal-Bench 2.0 and WebArena, and the authors are careful to describe this evidence as observational rather than as randomized ablation.

Its contributions are the four-paradigm evolutionary account, the six-component harness decomposition, a mapping from task properties to harness configuration, and an argument for evaluation that reports more than task success. It also proposes a value-aware formulation (see [[DefinedTerm/value-aware-agent-evaluation]]) that couples task value with cost, latency, risk and reliability constraints, and sketches [[DefinedTerm/agent-native-training]] and model–harness co-evolution as the direction beyond hand-designed runtimes.

## Key Points

- An LLM-based agent is written as a model layer coupled with an execution harness; in deployed multi-model systems the model layer is a set of backbones with heterogeneous capabilities, costs and context limits, and the harness must additionally decide which model acts at each step.
- The harness is decomposed into six coupled runtime responsibilities: observation interface, context manager, control loop, action interface, state and artifact store, and verification and governance layer. The survey stresses these are coupled rather than independently optimizable — stronger compression can reduce cost while weakening downstream verification, richer actions improve coverage while increasing governance pressure, and more persistent state improves continuity while introducing stale or conflicting evidence.
- Agent engineering is traced through four paradigms — prompt engineering, workflows and context engineering, harness engineering, and agent-native training with co-evolution — presented as a conceptual evolutionary lens in which all four coexist today, not a strict temporal partition.
- Model-centric scaling is argued to face two limits: a resource–performance boundary (the survey cites LLaMA 3.1 moving from 70B to 405B as increasing training compute from 7.0M to 30.84M H100 GPU hours for modest benchmark gains) and a measurement boundary (frontier releases clustering in a narrow range on saturated static benchmarks). These figures are reported from the cited work rather than measured here.
- Task structure, not application label, determines which harness component becomes the bottleneck. The survey uses three dimensions — task horizon, environment type and autonomy level — and gives a four-level complexity scale from single-step to open-ended, naming the L2-to-L3 transition as the most consequential.
- Across domains the primary bottleneck migrates: software engineering is described as verification-dominant, web and GUI interaction as grounding-dominant, scientific discovery as synthesis-dominant, medical assistance as safety-dominant, and embodied settings as control-dominant.
- On SWE-bench Verified the compiled table shows both effects: within one harness, backbone upgrades move SWE-agent + tools from 49.0% with Claude 3.5 Sonnet to 73.2% with Opus 4; within one model, harness choice moves Claude 3.5 Sonnet from 33.6% with SWE-agent to 53.6% with PatchPilot. The authors caution that the table is a synthesis of public evidence rather than a controlled factorial experiment, and that vendor rows are upper-envelope references.
- Scaffold complexity is reported not to predict effectiveness: under Opus 4.5, mini-SWE-agent — described as roughly 100 lines of Python — reaches 76.8% against the richer OpenHands + CodeAct 2.1 sandbox at 77.6%.
- On Terminal-Bench 2.0, among the 20 models with at least three observed harness results the median within-model accuracy range is 13.6%, and 14 of the 20 vary by at least 10% across harnesses. The survey pairs accuracy with operational profiles — median input tokens, median agent runtime and timeout rate — to argue that a score is interpretable only together with the runtime configuration that produced it.
- On WebArena the gap between a model-only baseline and a harnessed system is reported as larger still, with GPT-4o moving from 13.1% model-only to 54.6% under one browser harness.
- The survey argues evaluation should report task success alongside reliability, efficiency, latency, safety and process quality, and proposes value-aware agent optimization: maximizing expected task value weighted by success probability and process quality, subject to cost, latency, risk and repeated-run reliability constraints.

## Notes

The authors position the work against recent harness-focused surveys, saying their contribution is not another layer taxonomy or project catalog but an account of how the dominant engineering bottleneck migrates and how that migration should be evaluated empirically. A companion collection of the papers discussed is published at <https://github.com/ggjy/Awesome-Agent-Engineering>.

The survey is explicit about the limits of its own empirical evidence. Public submissions differ in prompts, versions, budgets and implementation details, so its comparisons are observational; model snapshots, reasoning settings and retry budgets are not always aligned across sources, so it recommends within-row-family comparisons and treats vendor-reported scores as an upper envelope rather than a controlled ablation. For the Terminal-Bench resource analysis it reports that dollar-cost fields cover only 15.2% of trial records, so monetary cost is not used for cross-harness claims. Its stated open problems include whether harness improvements transfer across task distributions and model families, how to keep self-evolution observable and revertible, and where the boundary between model design and system design should finally sit.
