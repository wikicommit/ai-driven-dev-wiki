---
title: "Curriculum Engineering"
type: "schema:DefinedTerm"
lang: en
tags: [model-training, synthetic-data, ai-native-software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2410.06107'
    hash: sha256:16a4b6cfd923d16a41de150fe7052965c2d6efabb533839e3bb60287694f1747
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "The systematic design, development and continuous refinement of curriculums of curated, organised, high-quality domain-specific knowledge used to train foundation models, pairing careful data curation with synthetic data generation instead of scraping internet-scale data."
---

Curriculum engineering, as defined in
[[ScholarlyArticle/towards-ai-native-software-engineering-se-3-0]], is the systematic design,
development and continuous refinement of curriculums that contain curated, organised and
high-quality domain-specific knowledge, used as a more efficient alternative to training foundation
models on vast amounts of unstructured, internet-scale data. It values high-quality data curation
coupled with synthetic data generation over what the paper calls blind scraping of internet-scale
data. A curriculum does not have to be designed by hand from top to bottom: humans can use AI to
kick-start it, revise it manually, and, once it is stable, use AI again to generate synthetic data
such as concrete examples that enrich it.

## Usage

The term appears in the paper's vision of [[DefinedTerm/software-engineering-3-0]], where the model
behind its code synthesiser, FM.next, is expected to be trained on a high-quality software
engineering curriculum — for example one inspired by the IEEE Software Engineering Body of Knowledge
(SWEBOK) — so that it shows uniform competence across requirements reasoning, architectural design,
implementation, testing, debugging and maintenance. The paper argues that a curriculum externalises
knowledge from the model itself, so that it can be reviewed, reorganised or augmented in response to
how the model performs, using observability data about where the model excels or underperforms. On
this view curriculums, rather than the models, represent the intellectual property, and they need to
be asset-managed and versioned so that they can be expanded and reused across models and use cases.

## When It Applies

The paper offers a reference recipe for designing and maintaining a curriculum, drawing on IBM's
InstructLab as a prominent example of a systematic approach. Design starts by defining objectives
and scope, identifying key domains and subdomains, and having domain experts outline core concepts,
tasks and expected input-output specifications. The curriculum is usually structured as a
hierarchical taxonomy, each node a task or knowledge area with examples, templates and evaluation
rules; InstructLab suggests branching the root into knowledge, foundational skills and composition
skills. Because the few manually curated samples at the leaves are often not enough for satisfactory
instruction following, taxonomy-driven synthetic data generation — for instance with a teacher
model — fills the gap. The curriculum is then tested for internal consistency and refined through
pilot testing and community contributions, with a data flywheel recommended so that curriculum
engineers change it to address problems observability data reveals, such as under-represented
areas, emerging trends in the data and concept drift.

It assumes that observability data about the model's performance is available to drive refinement,
and the paper itself treats designing an effective software engineering curriculum as an open
challenge. How well established the practice is: it is presented as one research group's proposed
strategy within a vision paper, supported by reference to recent systematic approaches such as
InstructLab rather than by a measured result of its own.

## Related Terms

- [[DefinedTerm/software-engineering-3-0]] — the proposed era whose models this approach is meant
  to train
