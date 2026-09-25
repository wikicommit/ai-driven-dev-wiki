---
title: "SkillsBench: Benchmarking How Well Agent Skills Work Across Diverse Tasks"
type: "schema:ScholarlyArticle"
lang: en
tags: [agent-skills, benchmarks, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2602.12670'
    hash: sha256:120b2b2642836eb5bfcd39ce25249bd93b8222b676ab83039dffbf583142ea3e
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An arXiv paper presenting SkillsBench, a benchmark that measures whether Agent Skills actually help LLM agents by running tasks under matched no-Skills and curated-Skills conditions, and reporting that curated Skills raise the average pass rate."
  datePublished: "2026-02-13"
  keywords: ["agent skills", "benchmark", "paired evaluation", "LLM agents"]
---

The paper describes [[DefinedTerm/agent-skills]] as structured packages of procedural knowledge that augment large language model agents at inference time, and observes that despite their rapid adoption there is no standard way to measure whether they actually help.

To fill that gap it presents [[Dataset/skillsbench]], a benchmark whose current inventory contains 87 tasks across 8 domains, each paired with curated Skills and deterministic verifiers. The paper's latest aggregate evaluation runs all 87 tasks under matched no-Skills and curated-Skills conditions for 18 model-harness configurations, and the authors present this paired evaluation as the foundation for rigorous measurement of Skill efficacy on agentic, expertise-heavy work.

## Key Points

- Curated Skills raise the average pass rate from 33.9% to 50.5%, an increase of 16.6 percentage points (a 25.5% normalized gain), across the 18 model-harness configurations evaluated.
- Gains vary by configuration, ranging from +4.1 to +25.7 percentage points.
- Focused Skills with at most three modules outperform larger or exhaustive bundles.
- Smaller models equipped with Skills can match larger models without them.
- The authors argue that SkillsBench establishes paired evaluation — the same tasks run with and without Skills — as the foundation for measuring Skill efficacy.

## Notes

The paper was first submitted to arXiv on 13 February 2026 and last revised on 14 June 2026 (version 4). It lists 77 authors and is filed under Artificial Intelligence (cs.AI).
