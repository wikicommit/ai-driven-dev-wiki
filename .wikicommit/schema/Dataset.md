---
wikicommit:
  base: https://schema.org/Dataset
  provenance: generate-interactive
  granularity:
    - Create a new page for a specific, named dataset or evaluation benchmark that is an independent subject and directly relevant to the wiki's theme (e.g. a benchmark used to measure coding-agent capability)
    - A dataset or benchmark mentioned only in passing (e.g. listed alongside several others with no independent discussion of what it measures or what results it produced) is an incidental mention, not an independent subject — do not create a page for it
    - Boundary with DefinedTerm — a Dataset is a concrete, named artifact with an identity and a maintainer (a task collection, corpus, or benchmark suite); the general evaluation methodology or metric it embodies is a DefinedTerm, not a Dataset
    - Boundary with SoftwareApplication — a Dataset is the data/task collection itself; a harness, runner, or agent that executes against it is a SoftwareApplication
    - A revised or filtered edition of an existing benchmark (e.g. a "Verified" or "Pro" subset) belongs on the parent benchmark's page unless the source treats it as an independently maintained artifact with its own construction method
    - creator names the organization or people who built the dataset; link each one that independently qualifies for its own [[Organization/slug]] or [[Person/slug]] page with a WikiLink, and list others as plain text
    - The body should describe what the dataset contains and what capability it is designed to measure, not restate every reported score
title: ""
type: "schema:Dataset"
lang: ""
sources: []
tags: []

properties:
  description: ""
  creator: "[[Organization/slug]]"
  datePublished: ""
  measurementTechnique: ""
  sameAs: ""
---

(2-3 paragraph overview: what the dataset contains, how it was constructed, and what capability it measures)

## Composition
(scale, task types, and how instances were collected or validated)

## Use in Evaluation
(how the dataset is used to evaluate systems, and known limitations such as contamination or scope)
