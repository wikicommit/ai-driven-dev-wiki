---
title: "Deployment overhang"
type: "schema:DefinedTerm"
lang: en
tags: [autonomy, human-oversight]
sources:
  - type: url
    url: 'https://www.anthropic.com/research/measuring-agent-autonomy'
    hash: sha256:ad91061ead4703b40288c2ad7e1f7a3bcccdeb8990451717ea2fbf1d6427addb
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A gap in which the autonomy AI models are capable of handling exceeds the autonomy they actually exercise in practice, as described by Anthropic's February 2026 study of agent autonomy."
---

A deployment overhang, as [[Report/measuring-ai-agent-autonomy-in-practice]] uses the term, is a
situation in which the autonomy AI models are capable of handling exceeds what they exercise in
practice — the latitude granted to agents in real deployments lags behind what they can handle.

## Usage

[[Organization/anthropic]]'s study draws the conclusion from two of its measurements of
[[SoftwareApplication/claude-code]]. The 99.9th-percentile turn duration nearly doubled between
October 2025 and January 2026, and rose smoothly across model releases rather than jumping with each
launch, which the authors read as a sign that existing models are capable of more autonomy than they
exercise. Among Anthropic's internal users, the success rate on the most challenging tasks doubled
between August and December while average human interventions per session fell from 5.4 to 3.3. The study contrasts its figures with external
capability assessments such as METR's, which measure what a model can do in an idealized setting with
no human interaction, while its own measurements capture what happens in practice, where Claude pauses
to ask questions and users interrupt. It stresses that the two kinds of metric are not directly
comparable, and that together they suggest in-practice latitude lags behind capability.

In this account the gap is not only a matter of what users permit: the authors attribute the growth in
autonomy to several possible factors, including power users building trust with the tool over time,
applying it to more ambitious tasks, and improvements to the product itself.

## Related Terms

- [[DefinedTerm/agentic-autonomy-levels]]
- [[DefinedTerm/human-in-the-loop]]
