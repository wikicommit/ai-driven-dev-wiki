---
title: "SWE-Compass: Towards Unified Evaluation of Agentic Coding Abilities for Large Language Models"
type: "schema:ScholarlyArticle"
lang: en
tags: [evaluation, agents, benchmarks]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2511.05459'
    hash: sha256:306904f768da56528a41e5c9652823b778a536de3b45569339cba85aa458105c
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "Introduces SWE-Compass, a 2,000-instance benchmark spanning eight task types, eight programming scenarios and ten programming languages, and reports an evaluation of ten large language models under the SWE-Agent and Claude Code agentic frameworks together with a taxonomy-based analysis of why their trajectories fail."
  abstract: "The paper argues that evaluating large language models for software engineering has been limited by narrow task coverage, language bias and insufficient alignment with real-world developer workflows, with existing benchmarks focused on algorithmic problems or Python-centric bug fixing. It introduces SWE-Compass, a benchmark unifying heterogeneous code-related evaluations into a structured, production-aligned framework of 2,000 instances curated from authentic GitHub pull requests, and benchmarks ten state-of-the-art models under two agentic frameworks, reporting a clear hierarchy of difficulty across task types, languages and scenarios."
  keywords: ["agentic coding", "benchmark", "software engineering evaluation", "large language models"]
---

This paper introduces [[Dataset/swe-compass]], a benchmark for evaluating the agentic coding
abilities of large language models, and reports an evaluation of ten models run on it under two
agentic frameworks. Its motivating argument is that existing evaluations fall short of real-world
software engineering: most remain restricted to single-file tasks, Python-centric bug fixing or
synthetic algorithmic problems, and even repository-grounded benchmarks converge on bug fixing as the
dominant evaluation axis, leaving feature implementation, refactoring, configuration and performance
optimisation underexplored. The paper argues that this narrowness prevents systematic capability
diagnosis and obscures whether strong performance arises from generalisable reasoning or from
artifact-specific adaptation.

The benchmark is built on four stated design principles — real-world alignment, comprehensive and
balanced coverage, a systematic taxonomy, and evaluation fidelity — and its taxonomy of eight task
types, eight programming scenarios and ten languages is itself derived empirically, through an
iterative active-learning procedure applied to repository-level coding discussions collected from
Stack Overflow and GitHub. The evaluation runs in fixed offline containers with networking disabled,
no retries, a single-attempt setting and standardised build and test commands per language, and uses
metrics chosen per task type: pass@1 for feature implementation, feature enhancement, bug fixing and
refactoring; a binary performance-optimisation score; line coverage for test case generation; and an
LLM-as-a-judge checklist score for code understanding.

## Key Points

- The benchmark's construction pipeline reports two figures that characterise how hard it is to build
  execution-backed evaluation data at scale: the initial automated Docker build success rate was
  around 2%, and an expert-assisted retry process in which 30 annotators inspected build logs,
  identified root causes and applied targeted fixes raised the overall retention rate to
  approximately 8%, yielding about 4,000 runnable images from roughly 50,000 high-quality pull
  requests.
- Across task types the paper reports a consistent but nuanced difficulty hierarchy: code
  understanding is among the strongest categories across models; feature enhancement and refactoring
  occupy a middle tier; feature implementation and bug fixing are harder, which the authors attribute
  to localisation and integration challenges; and test case generation and performance optimisation
  remain challenging without falling to single-digit averages.
- The two agentic frameworks come out complementary rather than one dominating. Claude-Sonnet-4 ranks
  first under both, at 32.9% macro-average with Claude Code and 31.8% with SWE-Agent, but among the
  five models evaluated under both frameworks only two score higher with Claude Code while three score
  higher with SWE-Agent. The authors attribute the split to mechanism: an edit-diff-execute loop
  favours investigative, multi-file tasks that reward iterative localisation at the cost of higher
  timeout exposure, while a sandboxed, editor-centric workflow performs better on well-scoped,
  deterministic tasks with lower tool overhead.
- Language-level results show a consistent cross-language stratification: JVM ecosystems and
  JavaScript score higher, TypeScript notably lower, systems languages (C, C++, Rust, Go) are harder,
  and Python sits mid-tier, which the paper partly attributes to open-source benchmarks over-indexing
  on difficult Python bug-fixing cases. The authors read the pattern as governed more by tooling
  determinism and diagnosability than by raw coding difficulty.
- The paper reports a relationship between effort and success rather than a simple ranking:
  improvements in score often coincide with higher average interaction turns, with diminishing
  returns beyond moderate turn counts, which it reads as evidence that future gains require better
  localisation and hypothesis pruning rather than more exploration.
- A post-hoc failure analysis, using an LLM-as-judge protocol over 600 sampled failed trajectories
  per model for three representative systems, develops a six-category taxonomy of root causes:
  requirement misinterpretation, inadequate testing, incomplete solution and side effects, technical
  knowledge gap, tool invocation error, and infinite loop. Requirement misinterpretation (30-34%) and
  incomplete solution with side effects (29-42%) together account for more than 60% of failures,
  while technical knowledge gap is consistently low at 5-8% — which the authors read as locating the
  core limitation in requirement grounding and holistic solution design rather than in basic coding
  proficiency.
- An analysis of several existing repository-level benchmarks, annotated against the same taxonomy,
  reports that those datasets are entirely focused on bug fixing, that application development
  dominates their scenario distribution, and that Python accounts for the large majority of their
  instances — the imbalance the new benchmark is built to address.

## Notes

The paper's quantitative comparisons should be read against its own stated setup: results come from a
single-attempt protocol with fixed decoding and turn and time limits, networking disabled and no
retries, so they measure performance under a constrained budget rather than best achievable
performance. The failure-mode analysis rests on an LLM-as-judge protocol with Claude-Sonnet-4 as the
judge, which the authors justify by citing prior work reporting high agreement between automated
judges and human experts; the paper's own future-work section calls for human adjudication subsets
and reliability audits for exactly this reason.

The authors' proposed directions include expanding scale and language coverage, harder long-context
settings stressing architectural coherence and cross-session memory, richer metrics that report
consistency and variance alongside central tendency, unified cost and efficiency reporting, and safe
online or incremental evaluation tracks with evolving repositories and dependency drift.
