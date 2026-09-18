---
title: "Toward Agentic Software Engineering Beyond Code: Framing Vision, Values, and Vocabulary"
type: "schema:ScholarlyArticle"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2510.19692'
    hash: sha256:26029fa1c5daea4d737d3df8de8ce30162aa038efc1a8c3d4f0285e7d072a7d8
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A position paper, accepted to the AGENT workshop at ICSE 2026, arguing agentic software engineering research should expand beyond code-centric activities toward a 'whole of process' vision spanning the full software engineering lifecycle, proposing a preliminary CRAFT set of values and principles, and offering guidance for designing agentic SE vocabulary."
  author: ["Rashina Hoda"]
  abstract: "The paper argues agentic AI is poised to bring a seismic paradigm shift to software engineering, and that while early visions of agentic SE focus primarily on code-related activities, early empirical evidence calls for considering a wider range of socio-technical activities and concerns. It contributes an expansion of agentic SE's scope beyond code toward a 'whole of process' vision grounded in SE foundations and evolution, a preliminary set of values and principles to guide community efforts, and guidance on designing and using well-defined vocabulary for agentic SE."
  keywords: ["Agentic software engineering", "process", "vision", "values", "principles", "vocabulary", "terminology", "Agentic AI"]
---

"Toward Agentic Software Engineering Beyond Code: Framing Vision, Values, and Vocabulary" is a position paper by Rashina Hoda, accepted to the AGENT workshop at the International Conference on Software Engineering (ICSE) 2026. It argues that early visions of agentic software engineering (SE) — using autonomous AI agents such as SWE-agent, Google's Jules, OpenAI's Codex, Cognition's Devin, AutoCodeRover, and Anthropic's [[SoftwareApplication/claude-code]] to carry out software engineering work — have focused primarily on coding-related activities (generation, review, debugging, repair, configuration), and contends that for agentic SE to become a genuine process-level paradigm shift rather than merely a coding accelerator, its scope must expand to cover the full SE lifecycle and its socio-technical concerns.

The paper grounds this argument in a review of SE's own historical evolution — from the Waterfall, Spiral, and V models through the Rational Unified Process to Agile, Lean/Kanban, and DevOps — observing that each of these prior SE process models took a "whole of process" approach spanning roles, practices, and artefacts rather than a single activity. It surveys emerging agentic SE frameworks, including the "agentic AI Software Engineer" role proposed by Roychoudhury et al., the unified software engineering agent ([[SoftwareApplication/useagent]]) proposed by Applis et al., [[DefinedTerm/structured-agentic-software-engineering]] (SASE) proposed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]], and the [[Dataset/aidev]] dataset of agentic pull requests, and notes that early empirical studies report agentic AI's limits in addressing teamwork, coordination, accountability, and culture, as well as separately-raised organizational adoption challenges and human-AI collaboration concerns.

Building on this foundation, the paper makes three contributions: a preliminary [[DefinedTerm/whole-of-process-vision]] for agentic SE that extends across the SE lifecycle with ethical alignment introduced as a new, first-order area; a set of [[DefinedTerm/craft-values-and-principles]] (Comprehensive, Responsible, Adaptive, Foundational, Translational) to guide community research and practice; and [[DefinedTerm/agentic-se-vocabulary-considerations]] for designing agentic SE terminology.

## Key Points

- Proposes that agentic SE needs a [[DefinedTerm/whole-of-process-vision]] spanning five high-level areas — Ethical Alignment, Requirements Engineering, Design, Development, and Operations — approached iteratively by human and agent actors at varying, human-controlled levels of AI agency, rather than remaining centered on coding alone.
- Proposes a preliminary set of [[DefinedTerm/craft-values-and-principles]] — Comprehensive, Responsible, Adaptive, Foundational, and Translational (CRAFT) — each paired with two guiding principles, to steer agentic SE research and practice.
- Offers [[DefinedTerm/agentic-se-vocabulary-considerations]] — relevance, coverage, acceptance, consistency, and philosophical alignment — noting that syntactic and semantic drift in terms such as "agentic AI software engineer" vs. "AI software engineer" vs. "agentic software engineer" is already apparent despite the field's youth.
- Surveys emerging agentic SE proposals, including the "agentic AI Software Engineer" role described by Roychoudhury et al., the [[SoftwareApplication/useagent]] described by Applis et al., and [[DefinedTerm/structured-agentic-software-engineering]] with its associated [[DefinedTerm/se-autonomy-levels]] hierarchy, observing that these visions, while necessary and welcome, remain primarily focused on one SE activity — coding.
- Cites early empirical findings that AI acts as a "personal accelerator" for coding, writing, and documentation tasks but has not been shown to fix teamwork issues, with its impact on coordination, accountability, and culture still unclear, and that current studies often address organizational adoption and human-AI collaboration only narrowly.

## Notes

The paper positions its vision, values, and vocabulary guidance as preliminary and non-exhaustive, explicitly intended to invite community feedback and collaboration rather than serve as a definitive agentic SE process model. It states that the field's ultimate shape may only become clear through longitudinal studies of agentic repositories and forums and in-depth empirical work (interviews, surveys, experiments) with agentic SE teams, drawing an analogy to how the Waterfall model's own sequential reputation emerged from how it was used in practice.
