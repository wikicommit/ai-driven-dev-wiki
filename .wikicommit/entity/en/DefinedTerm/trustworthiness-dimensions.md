---
title: "Trustworthiness Dimensions"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2602.06310'
    hash: sha256:46f38f583fd26c851dbe000e63a827534bfc88506117ab3f9d5423e0303e5cd8
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A multidimensional trustworthiness framework for AI software engineers, proposed by Aleti, Hoda, Ray, and Chen in [[ScholarlyArticle/trustworthy-ai-software-engineers]], spanning technical quality, transparency and accountability, epistemic humility, and societal and ethical alignment."
---

Trustworthiness dimensions, as proposed in [[ScholarlyArticle/trustworthy-ai-software-engineers]], are a set of properties the paper argues jointly determine whether an [[DefinedTerm/agentic-engineer]] can be relied on, grouped into four areas: technical quality, transparency and accountability, epistemic humility, and societal and ethical alignment. The paper argues that no single dimension is both necessary and sufficient for trustworthiness — a system is not made trustworthy or untrustworthy by any one dimension alone — and that trustworthiness instead emerges from configurations of dimensions that collectively justify reliance in a given setting.

## Usage

Technical quality covers correctness (whether outputs meet functional requirements) and reliability (delivering acceptable results consistently over time), along with performance, robustness to invalid inputs or stressful conditions, security against misuse and vulnerabilities, and cost spanning developer time, computational resources, and environmental impact. Transparency and accountability cover whether stakeholders can understand how and why decisions are made, traceability linking outputs to inputs and processes, auditability and reproducibility supporting verification, and accountability for justifying actions and decisions to different audiences. Epistemic humility concerns an agent's ability to communicate uncertainty, acknowledge its own limitations, and remain aware of potential biases, which the paper argues guards against overconfidence, misuse, and misplaced trust in complex or high-stakes settings. Societal and ethical alignment covers fairness, bias mitigation, privacy protection, regulatory compliance, safety, and sustainability, along with how an agent integrates into human teams and broader socio-technical contexts.

The paper states these dimensions apply at different levels — system, model, and output — and matter to different stakeholders (developers, organisations, and society) over both short- and long-term horizons, and that they are grounded in and extend prior work on trustworthy AI and on software engineering quality models such as SWEBoK. It also notes emerging work on automated trustworthiness oracles, which suggests it may be possible to automatically generate checks for properties such as robustness, fairness, or security to guide developers toward the aspects of a system that warrant closer inspection, though [[ScholarlyArticle/trustworthy-ai-software-engineers]] does not itself develop such techniques.

## Related Terms

[[ScholarlyArticle/trustworthy-ai-software-engineers]], [[DefinedTerm/agentic-engineer]], [[DefinedTerm/evidence-centric-inspection]]
