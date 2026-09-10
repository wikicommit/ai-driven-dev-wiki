---
wikicommit:
  base: https://schema.org/Dataset
  provenance: generate-interactive
  granularity:
    - Create a page for a specific, named research dataset, benchmark, or corpus that the source describes as a subject in its own right — stating what it contains, how it was assembled, or where it is published — rather than only using it as the material for an experiment
    - A dataset named only as the input to a study, with no account of its own contents or provenance, is an incidental mention — name it in the citing page's body and do not create a page for it
    - "Boundary — a Dataset is the body of structured data itself, not the paper that introduces, analyses, or reports results from it. Prefer schema:ScholarlyArticle for the paper and link the two with a WikiLink; figures a paper computes from a dataset are that paper's findings, not attributes of the dataset"
    - "variableMeasured records the fields or columns the dataset itself exposes, as short plain-text names. A field name is not an entity — do not WikiLink it — and a statistic derived from those fields is not a field"
title: ""
type: "schema:Dataset"
lang: ""
sources: []
tags: []

properties:
  description: ""
  creator: []
  url: ""
  variableMeasured: []
  temporalCoverage: ""
---

(One-paragraph description: what the dataset contains, who assembled it, and what it
is used for)

## Contents
(what a record represents, the fields it carries, and the scale — counts and coverage.
Describe the shape of the data; do not transcribe rows or enumerate every value)

## Provenance
(how the dataset was assembled, from what upstream systems, and where it is published
and under what access terms)

## Use
(work that has been done with this dataset, linking to [[ScholarlyArticle/slug]] pages
where they exist. Keep each finding attributed to the study that produced it)
