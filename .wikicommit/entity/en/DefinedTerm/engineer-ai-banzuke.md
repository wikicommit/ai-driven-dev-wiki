---
title: "Engineer AI Banzuke"
type: "schema:DefinedTerm"
lang: en
tags: [ai-adoption, industry, maturity-model]
aliases: ["エンジニア版AI番付"]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/63720/'
    hash: sha256:1947e46ef8628cb2d5de929e0803937c2252a6f49f386942dfe3ac85d4e667ac
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "CyberAgent's assessment of the AI-adoption maturity of its development organizations, which scores each organization on two axes and fourteen items and expresses the result as one of seven ranks modelled on a sumo banzuke."
---

The Engineer AI Banzuke (エンジニア版AI番付) is an assessment that [[Organization/cyberagent]] designed to
make visible how far each of its development organizations has taken AI adoption, as a development-specific
counterpart to the company-wide AI Banzuke. Rather than asking only whether an organization uses AI, it scores
maturity on two axes — "engineering quality and technical maturity" (scope of AI use, depth of automation,
division of roles between humans and AI, integration into the development workflow, results, incident
response and AI infrastructure) and "promotion structure and technical culture" (level of use within the
organization, tooling and guidelines, knowledge sharing, promotion structure, measurement of effects,
communication to the rest of the company, and alignment with goals and strategy) — across fourteen evaluation
items, and expresses the result as one of seven ranks named after the ranks of a sumo banzuke.

## Usage

The seven ranks run from makushita, where AI use stays at the level of individuals, through jūryō (starting to
copy other organizations' examples), maegashira (partially adapting AI to the organization), komusubi
(comprehensively adapting it), sekiwake (organizational success cases established) and ōzeki (standardization,
measurement and outward communication under way), up to yokozuna, an AI-first development organization. The
first round covered 44 development organizations. Each organization reported its own status, submitted
evidence supporting the report, and the operators checked that evidence against the evaluation items, with a
deliberation council reviewing cases where needed before ranks were finalised. A second round was planned for
announcement in October 2026.

## When It Applies

The operators present it as both an evaluation scheme and a diagnostic tool for development organizations
moving to AI-first ways of working, in support of CyberAgent's stated aim of automating the development
processes across the company by 2028. They chose two axes because they consider both technically advanced use
and the organizational capacity to spread it reproducibly necessary: a few engineers with advanced practices
that are not shared, or study sessions without AI in the actual development process, both leave room to grow.
Self-reporting was chosen so that working out one's own position would itself prompt thinking about AI
strategy, while evidence and deliberation were added because self-reports alone cannot ensure fairness. The
operators acknowledge that a ranking format risks the result taking on a life of its own, and say they
consistently emphasised clarifying what each organization should improve next rather than ranking it. All of
this is the operators' own account of a single company's first round; the source reports observed tendencies
rather than measured outcomes.

## Related Terms

- [[DefinedTerm/ai-maturity-levels]]
- [[BlogPosting/designing-and-running-the-engineer-ai-banzuke]]
