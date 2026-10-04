---
title: "Spec-Driven Development – Wer die Spec schreibt, bestimmt, was gebaut wird"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, product-management, requirements, ai-assisted-development]
sources:
  - type: url
    url: 'https://www.produktbezogen.de/spec-driven-development-und-product-management/'
    hash: sha256:c6789c811cbcf671428a3995222b1034a3e4469203258789d4c111c504d2ea85
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "An April 2026 German-language post by product manager Rainer Gibbert on produktbezogen.de, arguing that spec-driven development is essentially product discovery in a format engineering teams can use, and that product managers and UX should actively lead the discovery phase of the SDD workflow."
  author: ["Rainer Gibbert"]
  datePublished: "2026-04-29"
  publisher: "produktbezogen.de"
---

This post, published in German on the product-development blog produktbezogen.de, looks at
[[DefinedTerm/spec-driven-development]] (SDD) from the product-management side. Its author, a product
manager, starts from his own team's experience: since it began relying heavily on AI, implementation
has become noticeably faster and product management has started struggling to keep up, with
requirements that once had to be clear by the next sprint now needing clarification "yesterday". A
developer then pointed him to SDD, whose core thesis he summarises as [[DefinedTerm/vibe-coding]]
working only up to a point — on greenfield, manageable tasks — before iterations with an AI agent grow
longer and the context window fills up, with structured requirements written before implementation as
the remedy.

His first reaction, he writes, was mixed: developers seemed to be rediscovering that good software
needs good requirements, something the product and UX community has preached for years under the name
"product discovery". On reflection he came to see the moment not as a defeat for product and UX but as
an invitation, and the post sets out what SDD is, why it is more than a developer trend, and what role
product and UX can play in it.

## Key Points

- The post defines SDD as an approach in which a structured description, the spec, is written before
  any code and serves as guard rails for AI coding agents, which derive an implementation plan and
  tasks from it and then implement them. The underlying idea, as he puts it, is that the more precisely
  the intent is stated at the start, the less an agent heads in the wrong direction.
- Citing Birgitta Böckeler of Thoughtworks, it distinguishes spec-first, spec-anchored and
  spec-as-source variants (see [[DefinedTerm/spec-driven-development-levels]]) and reports her view
  that most teams and tools use spec-first.
- The author notes that a spec typically contains user stories in the "As a…" format, acceptance
  criteria in GIVEN/WHEN/THEN form, data models, technical dependencies and business context, and
  observes that this is essentially a good old product requirements document.
- He describes a structural mismatch: AI accelerates implementation dramatically, but capacity for good
  requirements work — discovery, requirements definition, stakeholder alignment — does not scale with
  it, so development either waits or starts from unclear requirements, both of which are costly.
- His central claim is that SDD is at its core product discovery, finally in a format development
  teams can work with. He maps the first phase of a four-phase SDD workflow (discover, design, tasks,
  implement) directly onto product discovery, the difference being that its outputs now land as
  Markdown files in the AI agents' coding context rather than in Confluence, Miro, Figma or Jira.
- Drawing on an article by Hari Krishnan about adopting SDD at enterprise scale, he endorses
  Krishnan's argument that treating SDD as a purely technical rollout wastes most of its potential and
  that teams developing specs together are structurally better placed than individuals optimising their
  prompts. He also relays the risk Krishnan calls "SpecFall", after "Scrumfall": SDD without real
  cross-functional collaboration turning into a graveyard of Markdown files.
- His recommendations for product and UX are to lead the discover phase rather than wait for developers
  to fill it, prepare discovery outputs in a spec-compatible form, bring the value of user research
  explicitly into specs, treat stakeholder alignment as quality assurance rather than a brake, and
  establish short joint spec reviews with engineering before an agent starts work.
- He concludes that SDD does not make product and UX faster, but changes the direction of pressure:
  good requirements become a precondition for working AI-driven development, which makes product and
  UX's contribution visible.

## Context

The post is an opinion piece written from a product manager's perspective and based on his reading
and his team's experience rather than on measurements. Its descriptions of SDD variants and of the
SpecFall risk are attributed to other authors' writing, which it cites.
