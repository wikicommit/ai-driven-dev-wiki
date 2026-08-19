---
title: "external scenarios"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, evaluation, spec-driven-development]
sources:
  - type: url
    url: 'https://sddbook.blob.core.windows.net/downloads/spec-driven-development.pdf'
    hash: sha256:7f897827f00db69ac4a15f3acea3826e5504b1600d0b785cdce210d5414f1eea
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An evaluation practice attributed to StrongDM in which success criteria are held outside the codebase so a coding agent never sees them and cannot optimise against them. Kevin Ryan compares the principle to a holdout set in machine learning."
---

External scenarios are success criteria held outside the codebase an agent works in, so that the agent never sees what it is being evaluated against. The practice is attributed by [[Person/kevin-ryan]] to [[Organization/strongdm]], which he reports moved evaluation outside its codebase entirely as one of two architectural innovations underpinning its [[DefinedTerm/dark-factory]] operation.

## Usage

The problem the practice addresses is that traditional tests live inside the codebase. An AI can see them and — whether by design or under optimisation pressure — can build code that passes the tests without exhibiting the intended behaviour. Ryan describes this as the same problem as teaching to the test, and compares the fix to a holdout set in machine learning: if the agent cannot see the success criteria, it cannot game them.

Ryan states that external evaluation, together with simulated environments, is directly relevant to the methodology his book sets out and recurs throughout it. The wider argument he attaches to it is that AI-native execution requires evaluation infrastructure most organisations have not built — and that this matters because practitioners' own perception of whether a tool is helping is unreliable. He cites the METR randomised controlled trial, in which experienced developers were measured 19% slower with AI while believing they were 24% faster, as the case for external measurement over subjective judgment.

## Related Terms

External scenarios are one of the two StrongDM innovations Ryan documents; the other is the use of [[DefinedTerm/digital-twin]] environments. Ryan lists scenarios as one member of the Five Artefact taxonomy his book proposes — spec, code, provenance, scenarios and tests. The evaluation discipline this belongs to is what he calls the second new bottleneck alongside specification quality; see [[DefinedTerm/spec-driven-development]] and [[DefinedTerm/verification-debt]].
