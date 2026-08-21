---
title: "Agentic Context Engineering: Evolving Contexts for Self-Improving Language Models"
type: "schema:ScholarlyArticle"
lang: en
tags: [context-engineering, agent-architecture, evaluation, agentic-loop]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2510.04618'
    hash: sha256:6b917acfae2be76706c1360bd37b74776f6c979139cfb5a5604b5f0ed5f78951
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An ICLR 2026 paper proposing ACE, a framework that treats an agent's context as an evolving playbook updated by incremental deltas rather than rewritten whole. It names two failure modes of prior context-adaptation methods — brevity bias and context collapse — and reports average gains of 10.6% on agent benchmarks and 8.6% on domain-specific ones."
  author:
    - "Qizheng Zhang"
    - "Changran Hu"
    - "Shubhangi Upasani"
    - "Boyuan Ma"
    - "Fenglu Hong"
    - "Vamsidhar Kamanuru"
    - "Jay Rainton"
    - "Chen Wu"
    - "Mengmeng Ji"
    - "Hanchen Li"
    - "Urmish Thakker"
    - "James Zou"
    - "Kunle Olukotun"
---

"Agentic Context Engineering" (ACE) is a paper published at ICLR 2026 by authors from Stanford University, SambaNova Systems, and UC Berkeley. Its subject is **context adaptation**: improving an LLM application by modifying its inputs — instructions, strategies, evidence — rather than its weights, which the paper takes as the dominant mode for agents and domain-specific reasoning.

Its diagnosis is that existing context-adaptation methods degrade the very thing they are meant to accumulate. It names two mechanisms. **Brevity bias** is "the tendency of optimization to collapse toward short, generic prompts," which the paper illustrates with prior work on prompt optimization for test generation where iterative methods repeatedly produced near-identical instructions such as "Create unit tests to ensure methods behave as expected" — sacrificing diversity, omitting domain-specific detail, and propagating recurring errors because optimized prompts inherit their seeds' faults. **Context collapse** is the sharper failure: when a model is asked to fully rewrite an accumulated context at each step, a large context tends to be compressed into a much shorter, less informative summary.

The paper's case study of collapse is a single striking data point. On the AppWorld benchmark, at step 60 the context held 18,282 tokens and achieved 66.7 accuracy; at the very next step it collapsed to 122 tokens with accuracy dropping to 57.1 — below the 63.7 baseline achieved with no adaptation at all. The authors are explicit that although they observed it through one particular method, "the issue is not specific to that method; rather, it reflects a fundamental risk of end-to-end context rewriting with LLMs, where accumulated knowledge can be abruptly erased instead of preserved."

## Key Contributions

- **Contexts as evolving playbooks.** ACE treats a context not as a prompt to be optimized but as a structured document that accumulates, refines, and organizes strategies over time, updated under what the paper calls a grow-and-refine principle.
- **A three-role division of labour.** A **Generator** produces reasoning trajectories for new queries, surfacing both effective strategies and recurring pitfalls; a **Reflector** critiques those traces to extract lessons, optionally refining them over several iterations; and a **Curator** synthesizes the lessons into compact delta entries. The paper attributes the separation to a specific design intent: a dedicated Reflector splits evaluation from curation, which prior monolithic approaches conflated.
- **Incremental deltas instead of monolithic rewrites.** The Curator's deltas are merged deterministically into the existing context rather than regenerating it, which is the direct structural answer to context collapse — nothing is rewritten, so nothing can be silently dropped. The paper notes multiple deltas can be merged in parallel, enabling batched adaptation at scale.
- **Reported gains without labelled supervision.** ACE is reported to outperform strong baselines by an average of 10.6% on agent benchmarks and 8.6% on domain-specific ones, across both offline adaptation (e.g. system prompts) and online adaptation (e.g. agent memory). The paper emphasises that it builds these contexts from execution feedback and environment signals rather than labelled data.
- **A leaderboard comparison.** On the AppWorld benchmark leaderboard, ACE is reported to surpass the top-1-ranked production-level agent IBM-CUGA, powered by GPT-4.1, while itself using an open-source model (DeepSeek-V3.1) — matching it on the overall average and surpassing it on the harder test-challenge split. The paper also reports fewer rollouts and lower adaptation latency than existing adaptive methods.

## Notes

The two failure modes this paper names are the more useful contribution for a reader tracking terminology, because they generalise beyond the framework proposed to fix them. Both concern *lossy* context maintenance, and both sit alongside the related failures recorded on [[DefinedTerm/context-rot]] — where the loss is of attention over material still present — and on [[DefinedTerm/governance-decay]], where a summarization step drops standing rules specifically. Context collapse is the closest of the three to compaction as [[DefinedTerm/compaction]] describes it, and the paper's structural answer, replacing rewrites with append-only deltas, is a different remedy from the ones that vendor documentation recommends.

The evaluation is on agent and domain-specific benchmarks — AppWorld for agents, financial-analysis benchmarks for domain knowledge — rather than on software engineering tasks, so its relevance here is to the [[DefinedTerm/context-engineering]] mechanisms rather than to coding-agent performance directly. The framework's own components are LLM calls, which means the Reflector and Curator are themselves subject to the biases the paper documents; the reported gains are the authors' own measurements of their own framework.
