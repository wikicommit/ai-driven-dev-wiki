---
title: "Evidence-Centric Inspection"
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
  description: "An inspection approach proposed by Aleti, Hoda, Ray, and Chen in [[ScholarlyArticle/trustworthy-ai-software-engineers]] in which developers evaluate selective signals and justifications of an AI software engineer's trustworthiness, rather than reviewing its raw outputs in full."
---

Evidence-centric inspection, proposed in [[ScholarlyArticle/trustworthy-ai-software-engineers]], is a shift away from artefact-centric inspection — where developers focus primarily on reviewing final outputs such as code — toward assessing whether sufficient justification exists to rely on those outputs. Under this approach, developers do not need to see everything an [[DefinedTerm/agentic-engineer]] produced or did; they need to see signals about whether its outputs align with requirements and constraints, whether its key decisions are grounded in defensible reasoning, and whether uncertainty, assumptions, and potential failure modes are explicitly communicated.

## Usage

The paper motivates evidence-centric inspection as a response to a selective visibility problem: agentic engineers operate through multi-step processes involving planning, tool use, intermediate decisions, and iterative refinement, and exposing every intermediate artefact and reasoning step is neither scalable nor useful for developers who cannot feasibly inspect everything an agent produces. It extends verification and validation (V&V) accordingly: alongside the correctness of outputs, it adds process-level verification, concerning whether an agent's planning and tool use are appropriate, and epistemic verification, concerning whether the agent accurately represents its own uncertainty and limitations; validation is likewise extended to whether an agent's behaviour remains aligned with evolving requirements and constraints. The paper argues traditional approaches such as testing and static analysis remain necessary but are insufficient alone, because they operate primarily on final artefacts, and calls for techniques that distil large volumes of agent activity into concise representations of key decisions, assumptions, and risks, and for traceability mechanisms linking generated artefacts back to requirements and intermediate steps.

## When It Applies

Evidence-centric inspection is proposed for human-AI software engineering teams where agentic systems generate increasing volumes of code and development artefacts, making exhaustive human inspection infeasible and risking cognitive overload and review fatigue if attempted. It assumes tooling exists, or can be built, to summarise, structure, and expose the relevant parts of an agent's internal process — its decisions, assumptions, and communicated uncertainty — rather than only its final output. The paper presents this as a new proposal in a 2026 vision paper rather than an established or implemented practice: it identifies designing such "trust interfaces," which determine what information to present to developers and when, as an open research gap rather than a solved problem, and calls for future empirical and design-oriented research on how developers can be supported this way.

## Related Terms

[[ScholarlyArticle/trustworthy-ai-software-engineers]], [[DefinedTerm/agentic-engineer]], [[DefinedTerm/trustworthiness-dimensions]], [[DefinedTerm/code-review-as-runtime-monitoring]]
