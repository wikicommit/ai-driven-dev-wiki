---
title: "Reversa"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, legacy-modernization]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A framework that applies reverse documentation engineering to convert legacy software into operational specifications for AI agents, labelling the resulting artifacts with traceability, confidence and gaps."
  applicationCategory: "Reverse documentation engineering framework"
  featureList: "Recovery of operational specifications from legacy code; artifacts labelled with traceability, confidence and explicit gaps; support for multiple coding engines"
---

Reversa occupies the inverse position to the other frameworks assessed in
[[ScholarlyArticle/from-prompt-to-process]]. It does not start from a new product idea but from legacy
systems whose operational knowledge is embedded in the code, and proposes
[[DefinedTerm/reverse-documentation-engineering]] to convert that software into operational
specifications for AI agents to consume. It is published both as a framework and as a paper, and the
comparative study that assesses it declares a conflict of interest: Reversa is authored by that
study's own author, who states it receives the same critical analysis and record of risks as the other
five frameworks.

## Capabilities

Reversa treats legacy code as a source of evidence and produces artifacts carrying traceability,
confidence and gaps. The assessing study identifies the confidence and gap labelling as the crucial
part: an agent tends to fill absences with plausible inferences, and the study describes the framework
as trying, by labelling uncertainty, to prevent a generated specification from seeming more reliable
than it is. The framework also emphasises
support for multiple coding engines.

## Adoption & Ecosystem

Under the [[DefinedTerm/six-dimension-process-taxonomy]], Reversa scores 2 on specification, 2 on
context, 0 on roles, 0 on execution, 1 on validation and 1 on portability — a total of 6 out of 12. The
validation score is partial on the strength of those confidence and gap labels; the study records no
test or gate alongside them. It is the only framework in the study to address the direction from legacy to
specification, and it is narrow on roles and execution. The scores express the study author's judgement
from official documentation, not an independent empirical measurement.

The conceptual argument the study draws from Reversa is that AI frameworks for software should not be
limited to greenfield work: many real environments are brownfield or legacy-first, and there the
central problem is not generating code from an idea but recovering operational contracts before letting
an agent modify the system. The approach connects to the established traditions of reverse engineering
and design recovery while swapping the main consumer of the resulting documentation — no longer the
human, but the agent that has to maintain, migrate or evolve the system.

The limitation the study names is generalisation: the evaluation still needs to grow to multiple
systems, languages, domains and levels of pre-existing documentation. Reversa was also included at the
threshold of the study's traction filter rather than comfortably above it, and its evidence base is
recorded as a preprint with partial independent academic evaluation and a declared conflict of interest.
