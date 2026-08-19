---
title: "AI adoption J-curve"
type: "schema:DefinedTerm"
lang: en
tags: [ai-assisted-programming, software-development-process, productivity]
sources:
  - type: url
    url: 'https://sddbook.blob.core.windows.net/downloads/spec-driven-development.pdf'
    hash: sha256:7f897827f00db69ac4a15f3acea3826e5504b1600d0b785cdce210d5414f1eea
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The DORA team's name for the pattern in which increasing AI adoption first depresses delivery throughput and stability before improving them. DORA's 2024 finding was that every 25% increase in AI adoption correlated with a 1.5% drop in delivery throughput and a 7.2% drop in stability."
---

The J-curve is the name the DORA team gave to the pattern in which increasing AI adoption initially depresses software delivery performance before it improves it. DORA — described in [[Book/spec-driven-development-ai-native-software-engineering]] as the largest annual study of software delivery performance, surveying over 39,000 professionals — found in 2024 that every 25% increase in AI adoption correlated with a 1.5% drop in delivery throughput and a 7.2% drop in stability.

## Usage

[[Person/kevin-ryan]] argues the dip is real rather than a measurement artefact. Evaluating AI suggestions takes time, and correcting "almost right" code — output that compiles, passes obvious tests, but hides a subtle defect — can take longer than writing it from scratch. He adds a reinforcing loop from the same reported data: 39% of developers reported low or zero trust in AI-generated code, so they review everything manually, which makes AI-assisted work slower, which confirms the distrust.

The strategic claim Ryan attaches to the curve is about how organisations misread it. Most leadership teams, he argues, interpret the dip as evidence that AI does not work and cut investment or slow adoption precisely when they should push through. On his account the J-curve is therefore "the mechanism by which a specification gap becomes a competitive gap" — and by the time the first group realises what happened, the distance will be very hard to close.

## Related Terms

Ryan pairs the J-curve with the METR randomised controlled trial as the two pieces of evidence that AI adoption without supporting practice underperforms; his prescription in both cases is the evaluation infrastructure discussed under [[DefinedTerm/external-scenarios]] and the specification discipline of [[DefinedTerm/spec-driven-development]]. The broader practice the curve measures adoption of is [[DefinedTerm/ai-assisted-software-development]].
