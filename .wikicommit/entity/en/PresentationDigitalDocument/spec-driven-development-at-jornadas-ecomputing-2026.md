---
title: "Desarrollo Guiado por Especificaciones @ Jornadas eComputing 2026"
type: "schema:PresentationDigitalDocument"
lang: en
tags: [specifications, education]
sources:
  - type: url
    url: 'https://speakerdeck.com/deors/desarrollo-guiado-por-especificaciones-at-jornadas-ecomputing-2026'
    hash: sha256:c11fad15161e89737cb90d0e5c9d1fe43f23aac1b7be0344c33ed8184ae832bb
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "Spanish-language slide deck from a talk at the Jornadas eComputing in Vitoria-Gasteiz on 3 July 2026, arguing that spec-driven development is the skill that lasts once AI writes the code, and that it should be taught in schools."
  author: ["Jorge Hidalgo"]
  datePublished: "2026-07-03"
  recordedAt: "Jornadas eComputing 2026"
---

This eleven-slide deck accompanies a talk Jorge Hidalgo gave at the Jornadas eComputing in Vitoria-Gasteiz on 3 July 2026, under the framing question of what should be taught in the era of AI. Its subject is [[DefinedTerm/spec-driven-development]]: the deck defines it as an approach in which the specification is the single source of truth and the code is a consequence or by-product of it, and its subtitle states the talk's thesis — why it should be taught in schools.

The deck's description on Speaker Deck notes that the SDD process shown, with its commands and skills, is published in a repository adapted from the [[SoftwareApplication/agent-skills]] repository so that it works on GitHub issues rather than on markdown files.

## Details

- **The problem.** The deck opens from the observation that AI already writes the code, and asks what is left to learn. It contrasts what used to matter — knowing a particular language, memorising exact syntax, writing every line of code and tests, mastering the "how" — with what matters now: deciding what is worth building, describing the problem and its acceptance well, judging whether the result is correct, and mastering the "what" and the "why". Code is presented as a means to an end, the management of information flows.
- **What SDD is.** Three principles are given: the "what" comes before the "how", defining the problem and desired result before thinking about the technical solution; the specification governs, being the only source of truth from which code, tests and documentation derive; and specifications are verifiable by design, each stating what "done well" means so that it can become tests and executable criteria. The deck adds that SDD should not be seen as a bureaucratic formality but as the key to long-term success.
- **The cycle.** Six stages are shown, each building on the previous one and each leaving evidence: `/spec` turns requirements into a specification (a markdown file or a GitHub/GitLab issue); `/plan` derives an implementation plan as tasks; `/build` has the agent implement a task, in guided or autopilot mode, producing code, unit and integration tests and documentation under version control; `/test` re-runs the available tests; `/review` asks the agent to review code or documentation, typically at pull-request time; and `/ship` asks the agent for a pre-production analysis, reported as a comment on an issue. The deck credits the cycle to the Agent Skills repository and notes that other SDD approaches are equally valid. It remarks that "it seems to work (on my machine)" should never have been enough.
- **Specifying versus improvising.** The deck sets "vibe coding" against specifying first. Starting to type is characterised by an unclear goal, rework along the way, "this isn't what I wanted", results that are hard to check, and knowledge that lives in one head; starting from the specification gives shared understanding, clear tasks, a known meaning of "finished", verifiability from the start, and a basis on which anyone, human or AI, can build.
- **Why now.** Agents build and people specify: AI generates code quickly and cheaply but needs a clear specification to do the right thing, so the bottleneck is no longer writing code but knowing what to build and why. The deck qualifies the cheapness claim as a general assumption whose overall return on investment is not yet clear. People define intent and priorities, judge whether the result is good, and decide what is delivered and when.
- **Why teach it in schools.** The deck argues that specifying is not a skill only for future programmers, listing clear thinking, decomposition, defining "done", verifying with evidence, collaboration and thinking before doing. It presents specification as a unifying principle that appears in any task — a recipe, an experiment, an essay, a project — and calls writing good specifications a life skill.
- **Getting started.** No AI is needed to teach SDD, the deck says, though it prepares students to work with it: start from a simple template of problem, objective and criteria for "done"; specify before starting in any subject; review specifications among peers for clarity and verifiability; and build, check against the criteria and iterate.

The closing slide condenses the talk into five ideas: SDD means the what and the why first, then the how; the specification is the source of truth from which everything else derives; in the era of AI, specifying is the skill that endures; it teaches clear thinking, decomposition and verification for everyone; and starting is cheap.
