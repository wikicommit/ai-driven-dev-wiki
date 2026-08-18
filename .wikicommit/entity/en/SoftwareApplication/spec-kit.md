---
title: "Spec Kit"
type: "schema:SoftwareApplication"
lang: en
tags: [ai-assisted-programming, spec-driven-development]
sources:
  - type: url
    url: 'https://github.github.com/spec-kit/concepts/sdd.html'
    hash: sha256:8eb0247a43c5afbc5b75f447d9f90202cdd390cf55fa951daad26cb7eedbad2f
review_status: pending
generated_at: "2026-08-18"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A specification-driven development toolkit, whose documentation defines and sets out the process of [[DefinedTerm/spec-driven-development]]."
  applicationCategory: "Specification-driven development toolkit"
---

Spec Kit is a specification-driven development toolkit. Its documentation defines [[DefinedTerm/spec-driven-development]] — a process in which specifications become executable and directly generate working implementations — and sets out the core philosophy, development phases, and experimental goals of that approach.

## Overview

Spec Kit deliberately does not prescribe how teams preserve or mutate the `spec.md`, `plan.md`, and `tasks.md` files after requirements change; its documentation treats that as a separate topic, covered under spec persistence models and under workflows for evolving specs in existing projects.

## Features

The documentation frames Spec Kit's work as research and experimentation with four stated goals: technology independence, so that applications can be created using diverse technology stacks and the process is not tied to specific technologies, programming languages, or frameworks; enterprise constraints, covering mission-critical application development, organizational constraints such as cloud providers, tech stacks and engineering practices, and enterprise design systems and compliance requirements; user-centric development for different user cohorts and preferences, supporting approaches ranging from [[DefinedTerm/vibe-coding]] to AI-native development; and creative and iterative processes, including parallel implementation exploration, iterative feature development workflows, and upgrade and modernization tasks.
