---
title: "Citation Discipline in Spec-Driven Development: A Cross-Model Empirical Study of Output Determinism and Automated Hallucination Detection in LLM-Generated Code"
type: "schema:ScholarlyArticle"
lang: en
tags: [spec-driven-development, verification, traceability, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.30689'
    hash: sha256:a18183a689a7171dd459d93148005c0a497297442e4c68cb3cd91953c958f93b
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A two-study controlled comparison of how three spec-driven development frameworks enforce traceability, finding that mandatory per-line requirement citations reduce output determinism while being the only mechanism that enables automated hallucination detection."
  author: ["Subham Panda"]
  datePublished: "2026-06"
  abstract: "Two controlled empirical studies comparing three SDD frameworks — traceSDD, Spec Kit and OpenSpec — across Claude Sonnet 4.6 (20 tasks, 240 implementations) and GLM-5-turbo (50 tasks, 600 implementations), measuring output determinism and automated hallucination detection rate."
  keywords: ["spec-driven development", "requirements traceability", "hallucination detection", "output determinism"]
---

"Citation Discipline in Spec-Driven Development" is a paper by Subham Panda, dated June 2026, asking whether forcing a coding agent to cite a requirement for every line of code it writes materially improves correctness, determinism and hallucination detectability. Its framing problem is one of accountability: unlike a human developer, an LLM cannot be asked afterwards to explain its decisions, and its output "appears plausible even when it introduces subtle deviations" — out-of-scope features, prior-art bleed-in from training data, over-engineering — which the paper says typically pass all automated tests while introducing unauthorized functionality.

## Key Findings

The comparison is between three approaches to traceability. **traceSDD** enforces mandatory inline citations on every line of code, binding each to a Tier-3 requirement point with hierarchical `REQ-XXX.Y.Z` identifiers, treated as verifiable claims: any REQ ID cited in code but absent from the specification is an automatically detectable orphan. **Spec Kit** ([[SoftwareApplication/spec-kit]]) enforces artifact-level consistency through its spec-plan-tasks chain, but on the paper's account the citation chain ends once implementation begins. **OpenSpec** uses post-hoc external trace maps in YAML sidecar files that link line ranges to spec IDs after the fact, without annotating source code.

The paper's headline result is a trade-off it reports replicating across two architecturally different models. **Citations reduce determinism**: the uncited condition produced significantly higher lexical similarity across independent sessions than the cited condition (Claude d = −0.76, p = 0.003; GLM d = −0.72, p < 0.001). **Only the cited condition enables automated hallucination detection**: a traceability detection rate (TDR) of 86.4% on Claude and 88.0% on GLM, against 0% for all three alternatives, with a 0% false positive rate in both studies. The author stresses what the uncited condition establishes — it used the identical REQ-format specification and still detected nothing, which the paper reads as proving that detection requires annotations in the code, not merely a structured specification.

Against the other two frameworks, traceSDD's advantage on determinism was partial: significantly better than Spec Kit (Claude d = 0.47, p = 0.049; GLM d = 0.42, p = 0.003) but not significantly different from OpenSpec (Claude d = 0.18, p = 0.44; GLM d = 0.14, p = 0.32). A fourth finding concerns the specification format itself: the uncited REQ-format condition significantly outperformed both external baselines (mean d = 1.02 against Spec Kit, mean d = 0.91 against OpenSpec), which the paper takes as evidence that structured REQ-format specifications provide a determinism anchor independent of any citation annotation.

The explanation the paper offers for the determinism penalty is citation placement variability: in each independent session the model must decide not only what code to write but where each citation goes — whether a function signature cites every requirement it implements or only the primary one, whether a multi-line conditional cites once or on each line — and these decisions, which the author notes have no correct answer, introduce systematic lexical divergence. The subgroup analysis found the penalty most pronounced for easy and small tasks.

## Context

The recommendations are tiered by setting. For production systems in regulated or high-stakes domains, the paper advises mandatory citations on the reasoning that 86–88% detection at 0% false positives justifies what it calls a moderate determinism cost of roughly 0.13–0.21 points of lexical similarity. For rapid prototyping it advises the uncited approach with a REQ-format specification, keeping the structural anchoring without the citation overhead. For teams weighing Spec Kit against OpenSpec, it states that Spec Kit's lower determinism and complete lack of automated detection make it the weaker choice on the dimensions measured, while explicitly allowing that "its developer experience and natural workflow may compensate in practice".

The paper is unusually forthcoming about its own limits. All implementations are Python at moderate complexity (50–1,000 lines), so production-scale tasks may behave differently. Two models is stronger evidence than one but still a subset of the landscape. Most consequentially, hallucinations were *injected* using known-fake REQ-099 identifiers, and the author notes that organic hallucinations may be subtler — in particular, a model that omits citations entirely for hallucinated code bypasses the orphan-REQ check altogether, which the Claude data showed happening in roughly 12% of hallucination instances, leading to a recommendation that the orphan-REQ check be supplemented with an uncited-line check. The determinism metric measures lexical similarity, which the author acknowledges conflates content with formatting even after normalisation, and the Claude study at N=20 was underpowered for some comparisons.

One thing the paper does not state is any affiliation between its author and the framework it finds strongest; readers weighing its recommendation for traceSDD have only the reported method and its pre-registered analysis to go on.
