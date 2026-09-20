---
title: "Faster Code, Deeper Debt? A Multivocal Literature Review on Technical Debt and Its Early Signs in LLM-Assisted Software Development"
type: "schema:ScholarlyArticle"
lang: en
tags: [technical-debt, multivocal-literature-review, code-quality, maintainability, governance]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.14796'
    hash: sha256:326808613b90c63916547135da3cc5027f45d992bef8b64cc8f926069d4d622c
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A multivocal literature review of 104 formal and grey sources on how LLM-assisted development contributes to technical debt, identifying six emerging LLM-specific debt categories alongside amplified traditional ones."
  author: ["Ramtin Ehsani", "Shriya Rawal", "Yuanfang Cai", "Preetha Chatterjee"]
  datePublished: "2026"
  keywords: ["large language models", "AI agents", "code generation", "technical debt"]
---

A multivocal literature review by four researchers at Drexel University, examining how LLM-assisted development contributes to technical debt and what strategies, tools, metrics and benchmarks exist to manage it. Its distinguishing method is the deliberate inclusion of grey literature alongside formal publications: the authors argue that a body of formal research on this topic is still emerging and takes time to reach publication, while practitioner sources provide timely real-world perspectives that complement the academic gaps.

The review analyses 104 sources — 31 formal and 73 grey — searched in January 2026. Grey sources were retrieved through a structured Google search via an API, then filtered by a 22-criterion quality framework across seven categories including authority, methodology and objectivity, with only sources scoring above half the maximum retained. Formal sources came from the ACM Digital Library, IEEE Xplore, SpringerLink and Elsevier ScienceDirect, screened against predefined inclusion and exclusion criteria and extended by forward and backward snowballing. Debt types were coded deductively against an established 13-category taxonomy, with inductive coding used to capture concepts unique to LLM usage.

The authors position the work as among the first to bridge a gap they identify in prior research: existing technical debt studies concentrate either on classical debt types or on ML-specific concerns such as model versioning and deployment, while very few examine the debt that arises when LLM outputs are integrated into software projects and must later be understood, reviewed and maintained.

## Key Points

- Among traditional debt types, code debt is by far the most frequently discussed (14 formal, 56 grey sources), followed by design debt (2 formal, 30 grey) and documentation debt (0 formal, 17 grey).
- The review identifies six debt categories not covered by the taxonomy it starts from: [[DefinedTerm/governance-debt]], [[DefinedTerm/prompt-debt]], [[DefinedTerm/fast-integration-debt]], data debt, ethical debt and [[DefinedTerm/provenance-debt]].
- Grey and formal literature emphasise different new categories: practitioner sources stress prompt, fast-integration, provenance, ethical and governance debt, while formal sources highlight data, prompt, provenance and ethical debt.
- The authors describe a domino effect in which fast-integration practices — rapidly generated code prioritising speed over quality — trigger cascading governance risks if left unmanaged.
- Governance debt is the most frequently discussed LLM-specific debt in grey literature (19 sources), defined here as the long-term oversight burden created when LLM-generated code or logic is incorporated into software systems, rather than governance of training or operating the models themselves.
- The review reports a study using a difference-in-differences design comparing GitHub projects adopting an LLM agent assistant against a matched control group, which found a statistically significant increase in development velocity alongside a 30% increase in static analysis warnings and a 41% increase in code complexity after adoption.
- A consistent mitigation recommendation appears in 58 of the 73 grey sources: follow a human-in-the-loop model, treating LLM outputs as drafts requiring review and refinement.
- Formal literature groups its strategies into three categories — data quality and standards alignment, prompt engineering, and tooling with human-in-the-loop frameworks — with 8 studies recommending improved preprocessing of training and input data, 7 addressing prompt design, and 10 emphasising integration into broader toolchains or reflective workflows.
- SonarQube is the most frequently mentioned detection tool, though the authors note it and similar linters are designed for general use and not optimised for the characteristics of AI-generated code.
- Both grey and formal literature revealed **no standardised benchmarks or datasets** for evaluating technical debt in LLM-generated code; the authors note this reflects a broader scarcity of comprehensive technical debt benchmarks even for human-written code.
- Existing metrics such as SonarQube rules are described across industry discussions as inadequate for AI-specific debt, able to surface syntax errors and some maintainability issues but not semantic accuracy, architectural fit or adaptability.

## Notes

The authors classify every source by how explicitly it frames technical debt, separating direct evidence — where the term or a recognised category appears in the title and frames the main discussion — from supporting evidence, where the source discusses associated phenomena such as code smells or maintainability issues and establishes an explicit connection to debt concepts. This classification is applied consistently across both literatures and used to guide interpretation.

Two of the review's definitions are deliberately narrowed relative to prior work, and the narrowing matters for reading the findings. Data debt here does not refer broadly to debt in model training pipelines or MLOps infrastructure, but to data-related conditions shaping LLM outputs that later create maintenance burdens once those outputs are incorporated into software. Governance debt is scoped the same way, to the oversight burden of incorporated code rather than to governance of the models.

Reliability is reported through inter-rater agreement: Cohen's kappa of 0.93 for the types of technical debt discussed, and a range of 0.90 to 1.00 for the remaining extraction questions, with a third author reviewing annotations for consistency. For grey sources the reported 100% agreement reflects consensus after reconciliation rather than an initial inter-rater statistic, which the authors state explicitly.

Among future directions, the authors call for expanding debt taxonomies beyond traditional categories, for longitudinal studies of how LLM-related debt accumulates over time — which they argue is now opportune given adoption since 2021 — and for research into socio-technical impacts, including a "prompt sprawl" problem in which prompts function as development artefacts yet are often undocumented or scattered across tools and repositories.
