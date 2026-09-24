---
title: "Spec-Driven Development for Agentic Software Engineering: Harnessing Human–Agent Teamwork"
type: "schema:ScholarlyArticle"
lang: en
tags: [spec-driven-development, agentic-software-engineering, software-engineering, human-agent-collaboration]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2609.00252'
    hash: sha256:5331d1eb219124b67deabb6640416e4b3ac07d3f4ede62ff19407f403d7d576d
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A conceptual paper, based on a multivocal literature review, that proposes Spec-Driven Development as the team-level discipline enabling agentic software engineering, distinguishes a technical harness around the agent from a methodological harness around the team, and sets out five human–agent interaction patterns."
  author: ["Jessica Díaz", "Joaquín Gayoso", "Andrea Cimminio", "Jorge Pérez"]
  datePublished: "2026-08-31"
  abstract: "The paper aims to establish the conceptual and methodological foundations of Spec-Driven Development as an enabling discipline for operating Agentic Software Engineering at team scale, and to characterize the harness through which teams govern agent behavior. Drawing predominantly on gray literature, it presents a socio-technical model of SDD in which specifications act as the contract substrate between humans and agents, an operational characterization of the harness that distinguishes the technical harness around the agent from the methodological harness around the team, and a typology of five human–agent interaction patterns."
  keywords: ["Spec-Driven Development", "Agentic Software Engineering", "Human–Agent Collaboration", "Agent Harness", "Context Engineering", "Persistent Knowledge"]
---

This paper argues that the move from AI-assisted practices such as [[DefinedTerm/vibe-coding]] to
agentic software engineering — in which autonomous agents are delegated goal-level tasks — is mainly a
socio-technical reconfiguration of the team rather than a technological event, and that
[[DefinedTerm/spec-driven-development]] is the discipline that makes the transition workable at team
scale. Its motivation is what it calls a productivity paradox reported from industry: individual output
rises with AI adoption while team-level throughput, review capacity and stability degrade, which the
authors read as Amdahl's law applied to the software life cycle — accelerating code production does not
accelerate the whole system when review, verification and integration keep their old capacity.

Because, in the authors' assessment, neither team-level SDD nor the harness as a team-governance
construct had yet been treated academically, the work is a multivocal literature review that draws
deliberately on gray literature (practitioner reports, talks, blog posts and open-source tooling)
alongside academic sources, synthesized interpretively rather than statistically. It contributes a
socio-technical model of SDD in which specifications are the contract substrate between humans and
agents; an operational characterization of the harness, split into a technical harness around the agent
and a [[DefinedTerm/methodological-harness]] around the team, illustrated with worked examples built
around a fictitious refund feature; and a typology of five human–agent interaction patterns through
which the human role is redefined.

The authors present the whole framework explicitly as a first step toward academic–industrial consensus
and as a set of falsifiable hypotheses, not as a validated theory, and close with a research agenda for
its empirical validation.

## Key Points

- The paper compares four paradigms — Agile & DevOps, GenAI-augmented SE, vibe coding, and agentic SE
  with SDD — along five socio-technical dimensions (unit of work, primary artifact, locus of cognition,
  accountability and team topology), arguing that the step to vibe coding is regressive on
  accountability, verification and onboarding while agentic SE under SDD recovers them in a
  transformed shape.
- It names five limitations that make vibe coding hard to scale as a team practice: non-reproducibility,
  non-auditability, non-transferability, review saturation and noise scaling — framed as failures of
  methodology rather than of practitioners.
- It defines SDD operationally through four commitments: every non-trivial planned change originates
  from a written specification treated as its contract; the specification is version-controlled with the
  code; artifacts are derived from it with explicit provenance; and where specification and artifact
  disagree, the specification is the source of truth and the disagreement is resolved by re-deriving the
  artifact or amending the specification, never by silent edits.
- It separates system specifications (the durable architecture, conventions and normative rules,
  materialized in agent rule files such as `AGENTS.md` or `CLAUDE.md`) from feature specifications (a
  specific change, created per task and archived once delivered), and distinguishes both from skills,
  which are procedural and loaded on demand rather than normative and always active.
- It rejects two misreadings of SDD — that it means "more documentation" and that it is a waterfall
  process — describing it as iterative over specifications first and code second.
- It distinguishes a technical harness (orchestration loop, tools, context management, memory,
  guardrails and verification loops), which it argues is transient and depreciates as models improve,
  from a methodological harness of eight team-owned mechanisms, which it argues appreciates over time;
  its practical conclusion is that teams should invest preferentially in the durable harness and treat
  tool selection as secondary.
- It identifies persistent shared knowledge — a store of decisions and rationale read at the start of
  every agent session and written at its end — as the mechanism that lets a collection of stateless
  sessions behave as a team.
- It proposes five human–agent interaction patterns, each an operation on the specification: briefing,
  consultation, review, norm encoding and orchestration, and describes the human's primary work shifting
  from producing code to governing the conditions under which agents produce it.
- It predicts four benefits (consistency, absorption of review load, transferability and compounding of
  the shared context) and five risks (talent bifurcation, cultural fracture, cost spiral, specification
  drift and platform lock-in), stressing that the benefits are predictions, not validated findings.

## Notes

The paper positions SDD against earlier specification-centric approaches — model-driven engineering,
behavior-driven development and domain-driven design — arguing that what is new is not the use of
specifications but a stochastic agent as the execution mechanism, with the human recast as orchestrator
and verifier. Several of its mechanisms explicitly adopt artifacts proposed in
[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]], including the
[[DefinedTerm/consultation-request-pack]] and the merge-readiness criteria of the
[[DefinedTerm/merge-readiness-pack]], and re-ground them in the specification: a consultation cites the
clause it cannot resolve, and every item of acceptance evidence discharges a clause of the originating
specification.

The authors state that their worked examples are illustrative constructions of their own, not reports
of specific industrial systems; that the central terms are recent and contested, so results under their
definitions may not transfer; that the motivating evidence skews toward web, SaaS and platform
engineering; and that SDD should be read as a governance discipline rather than a universal
prescription — for exploratory work whose requirements are genuinely unknown, a lighter discipline may
be more appropriate.
