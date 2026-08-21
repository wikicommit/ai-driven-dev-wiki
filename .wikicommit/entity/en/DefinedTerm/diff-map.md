---
title: "diff-map"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, context-engineering, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.17548'
    hash: sha256:becc2ac1a59aad4f9155e8968fd738e02ecb7dbf2e77a818df204daa4dfd3310
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A representation of a pull request's changes organised around logical units such as functions, classes and modules rather than sequential file diffs, with each unit anchored to the analytical reports and execution traces that produced claims about it."
  termCode: ""
  inDefinedTermSet: ""
---

A diff-map is a representation of a pull request's code changes proposed in [[ScholarlyArticle/rethinking-code-review-in-the-age-of-ai]], organised around logical units — functions, classes, modules — rather than presented as raw sequential file differences. Each unit is given a name and a reference point that ties the code to its evidence, with explicit traceability links to the analytical reports produced earlier in the review pipeline.

## Usage

Its stated purpose is provenance. The paper describes the representation as transforming review "from a memory exercise into a verifiable retrieval task, verifiable in the provenance sense: every reviewer-visible claim is anchored to its source-code location and to the report that produced it." In the framework it belongs to, all agents interact through the diff-map, which the paper calls a multidimensional substrate anchoring analytical reports, execution traces and requirement-alignment markers to specific code segments.

The problem it targets is stated in measured terms. That paper cites empirical work reporting that 54% of reviews fail to detect bugs because of change-understanding barriers, and that approximately 44.47% of review feedback is non-useful — compounded by cognitive load from large diffs, time pressure, and toxic communication patterns. A reviewer working from a sequential file diff has to reconstruct the logical structure of the change from memory; the diff-map's claim is that organising around logical units and attaching evidence to each removes that reconstruction step.

Practically, the reviewer can ask for fresh evidence against a specific unit — new runtime traces, or a re-evaluation of PR-to-issue alignment — and have it overlaid directly on the map rather than delivered as a separate report.

## Related Terms

The diff-map is the shared substrate of [[DefinedTerm/agentic-code-review]], and its anchoring discipline is the same idea as the source-citation convention used elsewhere in agent design under [[DefinedTerm/progressive-disclosure]]: give the consumer a condensed view plus a verifiable path back to the underlying material. It is one answer to the [[DefinedTerm/verification-bottleneck]] on the comprehension side rather than the capacity side.
