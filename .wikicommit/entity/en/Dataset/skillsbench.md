---
title: "SkillsBench"
type: "schema:Dataset"
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
  description: "A benchmark for measuring whether Agent Skills help LLM agents, made up of tasks across several domains that are each paired with curated Skills and a deterministic verifier."
---

SkillsBench is a benchmark, introduced in [[ScholarlyArticle/skillsbench-benchmarking-how-well-agent-skills-work-across-diverse-tasks]], for measuring how well [[DefinedTerm/agent-skills]] — structured packages of procedural knowledge that augment LLM agents at inference time — actually help on agentic, expertise-heavy work.

## Contents

The benchmark's current inventory, as described in the paper, contains 87 tasks across 8 domains. Each task is paired with curated Skills and a deterministic verifier, which lets the same task be run with and without Skills and scored the same way in both conditions.

## Use

[[ScholarlyArticle/skillsbench-benchmarking-how-well-agent-skills-work-across-diverse-tasks]] runs the 87 tasks under matched no-Skills and curated-Skills conditions for 18 model-harness configurations. It reports that curated Skills raise the average pass rate from 33.9% to 50.5%, with configuration-level gains from +4.1 to +25.7 percentage points; that focused Skills with at most three modules outperform larger or exhaustive bundles; and that smaller models with Skills can match larger models without them.
