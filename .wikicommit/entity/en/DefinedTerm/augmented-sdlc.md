---
title: "Augmented SDLC"
type: "schema:DefinedTerm"
lang: en
aliases: ["SDLC augmenté"]
tags: [sdlc, coding-agents, team-organization]
sources:
  - type: url
    url: 'https://blog.octo.com/organiser-une-equipe-de-developpement-a-l''ere-de-l''ia-partie-iii'
    hash: sha256:e22c6ff5cc8796eeca599798cb9ffe523e8ab45671155c15e5710a9f86016472
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A rereading of the Software Development Life Cycle for agentic AI, proposed in a 2026 blog series, that replaces its six sequential stages with five continuous moments and makes a team's shared body of knowledge, rather than code, the main asset the cycle produces."
---

The augmented SDLC (*SDLC augmenté*) is a proposal, set out in
[[BlogPosting/organizing-a-development-team-in-the-age-of-ai-part-iii]], to redefine the Software
Development Life Cycle for development in which AI agents carry out much of the execution. Rather than
inserting agents into an unchanged cycle, it redefines the cycle as a continuous loop of knowledge
transformation — "understand → make explicit → design → execute → verify → learn → enrich" — run by a
business-aligned team together with business experts, product managers, UX designers and agents. In
this cycle the software is described as the executable expression of a shared body of knowledge
(business intentions, domain models, decisions, specifications, rules, tests, architecture choices and
lessons from production), which humans continually enrich and agents use.

## Usage

The proposal organizes the cycle around five moments, which it presents as a continuous frame of
reference rather than new sequential stages:

- **Discover** — understand the business, users and opportunities, continuously rather than as an
  up-front analysis phase, through practices such as Product Discovery, UX research, Design Thinking and
  EventStorming, with agents capturing and synthesising workshops.
- **Design** — structure the knowledge into a business model and prepare the solution, with
  [[DefinedTerm/domain-driven-design]], [[DefinedTerm/example-mapping]] and Gherkin scenarios feeding
  [[DefinedTerm/spec-driven-development]] tools.
- **Build** — turn knowledge and decisions into software, with living specifications as the shared
  source of truth, several specialised agents working in parallel, and developers orchestrating them.
- **Validate & Deploy** — verify continuously that the software matches the expected behaviours, with
  living specifications, harness engineering, automated tests and continuous-integration pipelines;
  quality assurance, a separate stage in the traditional cycle, is folded into the preceding activity.
- **Learn & Evolve** — treat production as a permanent source of knowledge, with agents connected to
  observability platforms proposing improvements whose validation remains the team's responsibility.

The post maps each of the traditional six stages (Analyse, Design, Implementation, Quality Assurance,
Deploy, Support & Maintenance) onto a moment of the augmented cycle, and uses that correspondence to present the
augmented SDLC as a natural evolution of the traditional one rather than a break with it. The cycle is
meant as a governance framework local to each team that owns a business perimeter end to end, not as a
centralised process spanning the enterprise.

## When It Applies

- **Conditions.** It is proposed for organizations in which agents take on a growing share of
  engineering activities, and for teams aligned on a business perimeter whose life cycle they own.
- **Assumptions.** It assumes that the quality of the context given to agents is the main factor in
  their effectiveness, and that teams keep responsibility for the decisions that shape the product while
  agents accelerate execution.
- **Failure modes.** The post contrasts it with proposed AI SDLCs and Agentic Development Lifecycles that
  keep the historical structure and simply add steps or swap human actors for agents; it argues that
  these focus on accelerating execution and risk yielding software close to what competitors could
  produce, because models converge on the most widespread practices. It also warns against delegating to
  AI the decisions that define a product's identity.
- **Establishment.** The augmented SDLC is one author's proposal in a blog series, presented as the
  series' own position; it reports no evaluation.

## Related Terms

- [[DefinedTerm/domain-driven-design]]
- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/example-mapping]]
