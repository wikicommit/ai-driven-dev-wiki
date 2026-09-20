---
title: "From Human-Centric to Agentic Code Review: The Impact of Different Generations of Generative AI Technology on Review Quality"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, agents, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2607.13196'
    hash: sha256:1635571abac83780f1fe27a5b0def652bdd5addba148b5a72857e7b29a0c3c98
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An empirical study of 1.02 million reviewed pull requests from 207 GitHub projects across three code review eras — human-centric, LLM-assisted, and agentic — finding that agent-involved collaboration patterns speed up review decisions without improving review quality."
  author: ["Suzhen Zhong", "Shayan Noei", "Bram Adams", "Ying Zou"]
  datePublished: "2026-07-14"
  keywords: ["Software Engineering"]
  citation: "arXiv:2607.13196"
---

This paper studies how the arrival of generative AI in code review has affected review efficiency
and review quality. Its premise is that code review helps maintain software quality before code
integration while imposing a substantial workload on human reviewers, and that the process is
shifting from a primarily human one toward AI-supported review in which large language model
reviewers and AI agent reviewers participate alongside people. The authors state that empirical
evidence on the effects of that transition was lacking.

The study examines 1.02 million reviewed pull requests from 207 GitHub projects that transition
across three code review eras: human-centric review, LLM-assisted review, and
[[DefinedTerm/agentic-code-review]]. Within that material the authors identify three AI reviewer
adoption practices — Gradual AI Adoption, Rapid LLM Adoption, and Rapid AI Agent Adoption — and
model pull request review discussions as reviewer interaction sequences in order to characterize
how human, LLM, and AI agent reviewers collaborate during review.

The headline result is a split between efficiency and quality. Agent-involved collaboration
patterns — in particular reviews initiated by AI agents, or involving multiple AI agents — are
associated with faster review decisions under Gradual AI Adoption and Rapid AI Agent Adoption. The
authors report that these efficiency gains do not translate into better review quality. They also
find that review activity and pull request type remain important across all three eras, while
human-AI collaboration patterns become the strongest explanatory factor for review efficiency once
LLM and AI agent reviewers participate.

## Key Points
- Studies 1.02 million reviewed pull requests from 207 GitHub projects transitioning across three
  code review eras: human-centric, LLM-assisted, and agentic
- Identifies three AI reviewer adoption practices: Gradual AI Adoption, Rapid LLM Adoption, and
  Rapid AI Agent Adoption
- Models review discussions as reviewer interaction sequences to characterize human, LLM, and agent
  collaboration
- Finds agent-involved collaboration patterns — especially agent-initiated reviews and reviews
  involving multiple agents — associated with faster review decisions under Gradual AI Adoption and
  Rapid AI Agent Adoption
- Reports that these efficiency gains do not translate into better review quality
- Finds human-AI collaboration patterns become the strongest explanatory factor for review
  efficiency once LLM and agent reviewers participate, while review activity and pull request type
  remain important across all eras

## Notes

The association between agent-involved collaboration and faster decisions is reported as holding
under two of the three adoption practices the paper identifies, not uniformly. The study is
observational and drawn from GitHub projects, so its findings describe projects that made this
transition rather than establishing what caused the speed-up.
