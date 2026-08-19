---
title: "Cursor Context Bench"
type: "schema:Dataset"
lang: en
tags: [agentic-coding, benchmark, evaluation]
sources:
  - type: url
    url: 'https://cursor.com/blog/semsearch'
    hash: sha256:157e4d6a1147f217b21dc17ae116534a1fa413895b2162f592cc28adf71e1915
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An internal evaluation dataset maintained by Anysphere, focused on retrieving information in codebases where the correct answers are known. Cursor runs it over the most-used models in its product to measure the effect of retrieval tools on answer accuracy."
  creator: "[[Organization/anysphere]]"
  measurementTechnique: "Question answering over codebases against known correct answers"
---

Cursor Context Bench is an evaluation dataset that [[Organization/anysphere]] says it maintains, "focused on retrieving information in codebases with known correct answers". It appears in this wiki only through [[BlogPosting/improving-agent-with-semantic-search]], which uses it as the offline measurement behind that post's claims for [[DefinedTerm/semantic-search]].

## Composition

The source describes neither the dataset's size, nor its task types, nor how its instances were collected or validated. What it states is the shape of the task — retrieving information in codebases, with correct answers known in advance — and that the evaluation is run over all of the most-used models in [[SoftwareApplication/cursor]], including the company's own Composer.

## Use in Evaluation

The benchmark is used to compare two tool configurations for the same model: one in which semantic search is among the available tools and one in which it is not. Cursor reports that in every configuration semantic search significantly improved outcomes, and the headline figures it draws from these offline evaluations are 12.5% higher accuracy in answering questions on average, with a range of 6.5%–23.5% depending on the model.

The obvious limitation is provenance rather than method: the benchmark is maintained by the same company that reports the results and sells the feature being evaluated, and the source gives no indication that it is public or that anyone else has run against it. The same post's online A/B test on real user traffic produced considerably smaller effects than these offline figures.
