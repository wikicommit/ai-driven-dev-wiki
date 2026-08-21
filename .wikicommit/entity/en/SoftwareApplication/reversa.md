---
title: "Reversa"
type: "schema:SoftwareApplication"
lang: en
tags: [legacy-modernization, spec-driven-development, context-engineering, framework]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A framework that applies reverse documentation engineering to convert legacy software into operational specifications for AI agents, labelling the produced artifacts with traceability, confidence and gaps."
  applicationCategory: "DeveloperApplication"
  author: ""
  operatingSystem: ""
  softwareVersion: ""
  license: ""
---

Reversa runs the specification pipeline backwards. Rather than starting from a new product idea, it starts from legacy systems whose operational knowledge is embedded in the code, and proposes *reverse documentation engineering* to convert that software into operational specifications an AI agent can consume. [[ScholarlyArticle/from-prompt-to-process]] connects the approach to established traditions of reverse engineering and design recovery, with one substitution: the main consumer of the documentation is no longer the human but the agent that has to maintain, migrate or evolve the system.

## Overview

In the six-dimension taxonomy that paper proposes, Reversa is relevant above all in context and specification, with only partial validation. It scores 2, 2, 0, 0, 1, 1 across specification, context, roles, execution, validation and portability — a total of 6 out of 12 — and is the only framework in the set addressing the inverse direction, from legacy to specification, while remaining narrow in roles and execution.

## Features

It treats legacy code as a source of evidence and produces artifacts carrying traceability, confidence and gaps. The paper argues this labelling is the crucial part: because an agent tends to fill absences with plausible inferences, marking uncertainty is what stops a generated specification from appearing more reliable than it is. Reversa also emphasises support for multiple coding engines.

## History

The paper's conceptual reading is that Reversa demonstrates AI frameworks for software should not be limited to greenfield work, since many real environments are brownfield or legacy-first — in which case the central problem is not generating code from an idea but recovering operational contracts before letting an agent modify the system. Its stated main limitation is that evaluation still needs to extend across multiple systems, languages, domains and levels of pre-existing documentation; the comparison table records its dominant risk as "still limited empirical generalization."
