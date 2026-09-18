---
title: "Trustworthy AI Software Engineers"
type: "schema:ScholarlyArticle"
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
  description: "A 2026 vision paper arguing that AI software engineers should be evaluated as participants in human-AI software engineering teams, proposing a working definition of an 'agentic engineer' and a multidimensional framework for trustworthiness, and introducing evidence-centric inspection as a way to make that trustworthiness practically inspectable."
  author: ["Aldeida Aleti", "Rashina Hoda", "Baishakhi Ray", "Simin Chen"]
  datePublished: "2026"
  abstract: "Grounded in established software engineering definitions and recent research on agentic AI systems, the paper conceptualises AI software engineers as participants in human-AI software engineering teams and treats trustworthiness as a property of these systems and actors rather than a subjective human attitude. It identifies dimensions of trustworthiness spanning technical quality, transparency and accountability, epistemic humility, and societal and ethical alignment, and introduces evidence-centric inspection, under which developers evaluate selective signals and justifications of trustworthiness rather than raw outputs, with implications for verification, validation, and code review in human-AI software engineering teams."
---

"Trustworthy AI Software Engineers" is a 2026 vision paper by Aldeida Aleti and Rashina Hoda of Monash University, and Baishakhi Ray and Simin Chen of Columbia University. It responds to the rapid adoption of AI coding agents such as [[SoftwareApplication/claude-code]], [[SoftwareApplication/openai-codex]], and [[SoftwareApplication/kiro]] by asking what it means for an AI agent to be considered a software engineer at all, and then what would make such an agent trustworthy. The paper grounds its argument in established definitions of software engineering from IEEE, ACM, and the Software Engineering Body of Knowledge (SWEBoK), which characterise the field as far more than programming. It further notes that empirical studies of professional practice show a substantial portion of day-to-day work involves non-coding activities such as eliciting and negotiating requirements, analysing specifications, reviewing and maintaining code, coordinating with stakeholders, and documenting design decisions.

The paper distinguishes trust — a human decision or disposition to rely on an AI system — from trustworthiness, the properties of the system that justify that reliance, following a distinction it draws from Pink et al.'s work on trust and AI software practitioners. It argues that because agentic systems plan tasks, use tools, make intermediate decisions, and collaborate with human teammates across the software engineering lifecycle, trustworthiness must be understood more broadly than for conventional code-generation models: not only in terms of output quality, but also the soundness of decision-making, transparency, accountability, safe operation under uncertainty, and alignment with human intentions and team norms.

## Key Points

- Proposes a working definition under which an AI agent qualifies as an [[DefinedTerm/agentic-engineer]] only if it can handle software engineering tasks beyond coding, demonstrate agency through planning and tool use, collaborate within human workflows, and respect human values and accountability.
- Frames trustworthiness as a system property distinct from subjective trust, following Pink et al.'s trust/trustworthiness distinction, and argues no single dimension of trustworthiness is both necessary and sufficient on its own.
- Introduces a set of [[DefinedTerm/trustworthiness-dimensions]] for agentic software engineers, spanning technical quality, transparency and accountability, epistemic humility, and societal and ethical alignment.
- Proposes [[DefinedTerm/evidence-centric-inspection]], a shift from reviewing an AI agent's raw outputs (artefact-centric inspection) toward evaluating selective signals and justifications of trustworthiness, motivated by the infeasibility of exhaustive human review as agentic systems generate growing volumes of code.
- Extends verification and validation with process-level verification (whether an agent's planning and tool use are appropriate) and epistemic verification (whether the agent accurately represents its own uncertainty and limitations).
- Proposes [[DefinedTerm/code-review-as-runtime-monitoring]], reframing code review in human-AI teams as a continuous activity in which deployed code is treated as provisional and AI agents monitor production behaviour.

## Notes

The paper builds on prior work characterising trust in AI-assisted software engineering, including Khati et al.'s identification of ability, benevolence, and integrity as attributes of trustworthiness for coding models, but argues that agentic systems — which plan, use tools, and make intermediate decisions rather than only generating or completing code — require a broader framing of trustworthiness than conventional coding models. It is presented as a short vision paper with no accompanying empirical study (its own Data Availability statement notes there are no data available), and it closes by calling for future empirical and design-oriented research on trust-aware development practices, verification strategies, and human-AI collaboration models.
