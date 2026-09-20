---
title: "A Tertiary Review of Large Language Model-Based Code Generating Tasks: Trends, Challenges, and Future Directions"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-generation, tertiary-review, evaluation, benchmarks, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.25536'
    hash: sha256:84c75544b09d7855a70f7e1f4cfdd0942a5ef7c015bc8053143fd65c3c23992d
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A tertiary review synthesising 30 secondary studies on LLM-based code-generating tasks, mapping their reported effects onto an adaptation of the HELM evaluation framework and onto SWEBOK knowledge areas."
  author: ["Muslim Chochlov", "Michael English", "Jim Buckley"]
  datePublished: "2026"
  keywords: ["systematic literature review", "large language models", "software engineering", "code generating tasks"]
---

A tertiary review — a systematic review of secondary studies — by three researchers at the University of Limerick, consolidating what existing surveys and systematic reviews report about large language models applied to code-generating tasks. Its motivation is that while reported results are promising, the broader effects of applying LLMs to real-world development remain insufficiently understood, and existing tertiary work is either too broad, confined to a subset of tasks, or focused on cross-task aspects such as prompt engineering.

The review follows Kitchenham's systematic review methodology and SEGRESS reporting guidelines, searching IEEE Xplore, the ACM Digital Library, Scopus, DBLP, Web of Science and Google Scholar, and combining database querying with structured snowballing. It identifies 30 secondary studies published between 2017 and 2025. Two methodological contributions accompany the synthesis: a description of how an LLM was used reliably as a first-pass screener during snowballing, and an adaptation of the Holistic Evaluation of Language Models (HELM) framework — originally designed for natural-language evaluation — to software engineering contexts, by retaining its multi-measure design and redefining its scenarios around task, programming language and application type or domain.

The review's stated conclusion is that LLM-based code-generating tasks constitute a fast-maturing yet unevenly evaluated research area, highlighting the need for domain-aware model improvements and for holistic, standardised evaluation that addresses efficiency and its associated costs.

## Key Points

- The authors adopt an umbrella definition of a **code-generating task** as a software engineering task whose primary output is an automatically generated code artefact intended to be compiled or interpreted and executed — explicitly excluding tasks that produce only non-executable text such as inline comments, docstrings or documentation.
- The landscape has expanded quickly and shifted in kind: from a single secondary study in 2022, to 6 in 2023, to 17 in 2024, with the proportion of self-reported systematic reviews and mapping studies rising from 0% in 2022–2023 to 47% in 2024 and 83% in the first half of 2025.
- The authors read a sign of saturation in the numbers: while secondary studies nearly tripled from 2023 to 2024, the primary studies they collectively cover grew only from 1,491 to 1,724, which they interpret as maturation plus the onset of redundancy across secondary studies.
- In SWEBOK terms the field is concentrated: Software Construction is in scope for 25 of the 30 studies, followed by Software Maintenance (14) and Software Security (11), with the intersection analysis showing a strong LLM × Software Construction cluster.
- On **accuracy**, the evidence divides by study quality in a way the authors highlight: of 18 studies reporting on it, 8 lower-quality studies emphasise improvements, while 11 higher-quality studies either adopt a cautious perspective (7) or report poor accuracy outcomes (4).
- Higher-quality studies attribute inflated accuracy figures to dataset issues including code duplication and data leakage, note that metrics often fail to capture semantic correctness — producing syntactically correct but semantically incorrect code — and report that the same model can perform well on HumanEval while performing poorly on more diverse or real-world datasets.
- On **robustness**, a consistent view emerges across all 16 studies reporting on it, and across all quality bands: robustness is frequently overstated and remains fragile under realistic conditions, sensitive to dataset overlap, prompt and configuration changes, and decoding parameters such as temperature, with limited transfer across tasks, datasets and languages.
- On **efficiency**, the majority of the 14 reporting studies highlight computational, economic and energy costs, with suggested mitigations confined to improved training strategies and hardware acceleration.
- **Toxicity** — reinterpreted for code contexts as insecure patterns, vulnerabilities or licence-violating fragments — is addressed in only 8 studies, and **bias** in only 2, while **calibration** and **fairness** were not explicitly addressed by any study in the set.
- When task labels are consolidated, patch generation and repair is the most frequently reported code-generating task (22 studies), followed by code generation (20), code translation (9) and code completion (8).
- Reporting of HELM scenario dimensions is markedly uneven: almost all 29 studies report the task, only 8 specify programming languages, only 2 specify application types, and none provide details on the application domain.
- Among integration challenges, Economics is the most frequently reported category (10 studies), followed by Tooling & Workflow and Evaluation & Benchmark Validity (7 each).

## Notes

The authors are explicit that quality assessment was used to guide synthesis rather than to filter the set: all 30 papers were retained for descriptive mapping, with quality noted when drawing conclusions. Scored against DARE criteria, the distribution was 9 low, 8 medium and 13 high, giving an average of 2.45 — which the authors describe as comparable to other tertiary reviews.

Reliability safeguards are reported throughout. Inter-rater agreement on search-string screening reached Fleiss' kappa of 0.85, and on inclusion/exclusion decisions 0.86. An LLM was used as a first-pass screener across 2,769 snowballed records; validating it on a 100-record sample gave precision of 0.77 and recall of 1.00, with Cohen's kappa of 0.83 against human decisions. For the qualitative extractions behind three of the research questions, an extractor–checker strategy produced quote correct rates of 1.00 and label accuracies between 0.95 and 0.98.

Two observations about venues are worth noting alongside the quality scores. Journals carried 13 of the 30 studies, 7 of 8 journal venues ranked Q1 in Scimago, and journals had the highest average quality score at 2.77 — but arXiv preprints, at 9 studies, recorded the second-highest average at 2.39, which the authors read as some preprints nonetheless following a rigorous systematic approach.

The authors note that People & Process challenges do not map cleanly onto existing technical evaluation frameworks such as HELM or ISO/IEC 25010, which they describe as a known gap in current taxonomies with respect to human and organisational factors.

The protocol, search strings, screening rules, extraction forms, analysis scripts and curated dataset are publicly released by the authors.
