---
title: "Reverse Documentation Engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agents, legacy-modernization, spec-driven-development]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Converting legacy software into operational specifications intended for an AI agent to consume, running the specification-driven direction in reverse: from existing code to contract, rather than from intention to new code."
---

Reverse documentation engineering is the practice of recovering operational specifications from legacy
software so that an AI coding agent has a contract to work from. It runs
[[DefinedTerm/spec-driven-development]] backwards: instead of turning a human intention into artifacts
that guide the agent toward new code, it turns existing code into artifacts that describe what the
system already does. [[ScholarlyArticle/from-prompt-to-process]] presents it as the complementary
extreme to greenfield specification-driven work, and identifies
[[SoftwareApplication/reversa]] as the framework in its sample that implements it.

## Usage

The approach connects to the established traditions of reverse engineering and design recovery, but
swaps the main consumer of the documentation it produces: no longer the human reader, but the agent
that needs to maintain, migrate or evolve the system. Legacy code is treated as a source of evidence,
and the artifacts the practice produces carry traceability back to that evidence, together with
explicit confidence and gap labels.

Those labels do the load-bearing work. An agent tends to fill absences with plausible inferences, so a
specification recovered from code and presented without qualification can read as more reliable than
its evidence supports. The study describes the framework as trying, by labelling uncertainty, to
prevent a generated specification from seeming more reliable than it is. The study also scores the
approach only partially on validation, recording the confidence and gap labels as the validation it
offers and naming no test or gate alongside them.

## When It Applies

It applies to brownfield and legacy-first environments — which the study says many real environments
are — where the central problem is not generating code from an idea but recovering the
operational contracts before letting an agent modify a system whose operational knowledge is embedded
in its code rather than written down separately.
Where a greenfield specification framework assumes there is an intention to capture, this assumes
instead that the knowledge already exists, embedded in code, and that it can be extracted.

Its weak points as characterised by the study are narrowness of scope and thinness of evidence. The
practice as implemented addresses specification and context strongly, but the study records it as
narrow in roles and execution — it scores its one implementation 0 on both — so the approach as
realised recovers the contract without organising the work that follows. Its
evaluation
still needs to grow across multiple systems, languages, domains and levels of pre-existing
documentation before its generality is established.

How well established it is depends heavily on who is asking. The study places the approach in the
established traditions of reverse engineering and design recovery, which it treats as long-standing;
directing their output at an agent rather than a human is the new part, and it rests here on a single
framework and a preprint whose author also wrote the study that assesses it — a conflict of interest
the study declares.

## Related Terms

- [[SoftwareApplication/reversa]] — the framework that implements this practice
- [[DefinedTerm/spec-driven-development]] — the direction this one inverts
- [[ScholarlyArticle/from-prompt-to-process]] — the comparative study that positions the two against
  each other
- [[DefinedTerm/six-dimension-process-taxonomy]] — the instrument under which this approach's narrow
  coverage of roles and execution is recorded
