---
title: "Organiser une équipe de développement à l’ère de l’IA - Part III"
type: "schema:BlogPosting"
lang: en
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
  description: "Part III of a French-language series on blog.octo.com about organizing a development team in the age of AI, dated 5 July 2026. It revisits the Software Development Life Cycle as a governance framework for agentic development and proposes an \"augmented SDLC\" in which a shared body of knowledge, rather than code, is the main asset."
  author: ["Bruno Boucard"]
  datePublished: "2026-07-05"
---

The third part of this series asks how to organize a software product's whole life cycle once AI takes
over a growing share of engineering activities. After recapping part II — in which Domain-Driven Design,
Behavior-Driven Development and Spec-Driven Development form a continuum that turns business knowledge
into living specifications — it turns to the Software Development Life Cycle (SDLC), a framework it dates
to the 1960s, and argues that agentic development makes that framework more relevant rather than less.

The post's diagnosis is that many companies first treated agentic AI as a tooling change, giving
developers agents without changing practices, organization or knowledge, with disappointing results:
heavy token consumption, inconsistent implementations, hard-to-control quality and, in some cases,
initiatives abandoned over cost. It links this to *vibe coding* practised with little control, which it
says has produced code that is hard to understand and evolve — sometimes called "AI slop". Its answer is
to reread the SDLC as a governance framework local to each business-aligned team, and to redefine it as
the [[DefinedTerm/augmented-sdlc]], whose purpose is to create, structure, validate and continually
enrich the body of knowledge that humans and agents share.

## Key Points

- The post describes the traditional SDLC as six stages — Analyse, Design, Develop, Quality Assurance,
  Deploy, Support & Maintenance — and argues that it is independent of any method: agile, DevOps and
  Continuous Delivery renewed how it is implemented rather than replacing it.
- It holds that the SDLC answers the question of "what" rather than "how", which is why its stages must
  now be made explicit in how they are carried out when agents do much of the execution.
- It draws on strategic [[DefinedTerm/domain-driven-design]] to cut a system along business boundaries
  into subdomains and bounded contexts, and on Team Topologies to organize teams around those boundaries
  according to their cognitive load, citing Conway's law as the reason organizational and software
  boundaries should be aligned.
- It argues that agents raise a team's execution capacity without raising the complexity humans can
  master, so the limit on team size moves from execution capacity to the cognitive load a team can absorb.
- It calls the mechanisms that guide, constrain and verify agents' work an "AI harness", and states the
  principle that the more autonomous agents become, the more explicit, structured and verifiable their
  environment must be.
- It proposes five continuous moments for the augmented SDLC — Discover, Design, Build, Validate &
  Deploy, Learn & Evolve — forming a loop of "understand → make explicit → design → execute → verify →
  learn → enrich", with Quality Assurance folded into the preceding activity.
- It describes practices for each moment, from EventStorming, Continuous Discovery and the Opportunity
  Solution Tree in discovery, through CRC cards, Example Mapping and Gherkin scenarios feeding
  Spec-Driven Development tools such as GitHub Spec Kit in design, to agents connected to observability
  platforms in the learning phase.
- It warns against delegating to AI the decisions that make up a product's identity — its purpose,
  business strategy, user experience, business model and structuring architecture choices — on the
  grounds that models converge on the most widespread practices, so AI amplifies a competitive advantage
  rather than creating one.
- It criticises many proposed AI SDLCs and Agentic Development Lifecycles (ADLC) for keeping the
  historical structure and adding steps or replacing human actors with agents, focusing on accelerating
  execution while leaving implicit the activities that build shared business understanding.

## Context

This is the third part of a series and refers back to part II, published in two halves. It is written
as the author's argued position, with no measurements reported. Related posts in this wiki:
[[BlogPosting/software-development-in-the-age-of-ai-agents]] and
[[BlogPosting/organizing-a-development-team-in-the-age-of-ai-part-ii-2]].
