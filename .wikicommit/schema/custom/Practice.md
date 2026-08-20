---
wikicommit:
  base: https://schema.org/DefinedTerm
  provenance: manual
  rationale: >-
    Schema.org has no general type for a way of working. Its only "know-how as an entity"
    types are in the health vertical (MedicalProcedure, MedicalGuideline and their kin) and
    were never generalized; HowTo is an ordered step sequence shaped by the recipe/DIY use
    case (its own properties are prepTime, supply, tool, totalTime, yield), TechArticle and
    BlogPosting are the documents that describe a practice rather than the practice itself,
    and DefinedTerm is a term. This wiki's subject is AI-assisted development practice, so
    the thing a reader most often needs — should I adopt this, under what conditions, and
    how strong is the evidence — has no standard home. base names DefinedTerm as the nearest
    real parent (both are Intangible, not CreativeWork), so that dropping this custom type
    later means demoting these pages to DefinedTerm rather than restructuring them.
  granularity:
    - Create a page for a reproducible way of working that a practitioner would decide whether to adopt. The reader's question must be "should I do this, and when" — not "what does this mean"
    - A phenomenon or problem the practitioner suffers rather than performs is a DefinedTerm, not a Practice (e.g. context rot, verification debt). A component or mechanism that exists in the system is also a DefinedTerm (e.g. agent harness, subagents)
    - Setup or installation steps for one specific tool are not a Practice — record them in that tool's [[SoftwareApplication/slug]] page. A way of working that only makes sense with one vendor's product is usually that product's page, not a Practice
    - Do not create a Practice page from a single passing mention. The source material must describe how the practice is actually carried out, not merely name it
    - Boundary with HowTo: HowTo is a self-contained ordered sequence of steps toward one outcome. A Practice states judgment criteria — when it applies, what must be true first, how it fails — and is not reducible to a step list. If the page would be numbered steps and nothing else, it is a HowTo
    - Boundary with TechArticle/BlogPosting: the document describing a practice is a TechArticle or BlogPosting; this page is the practice itself, synthesized across however many documents describe it
    - description is a 2-3 sentence statement of what the practice is and what it achieves. Keep the fuller account in the body
    - appliesWhen states the conditions under which the practice is worth doing, and — where the sources say so — the conditions under which it is not. Both halves matter; a practice with no stated limits is usually under-sourced rather than universally applicable
    - precondition states what must already be in place for the practice to work at all (a test suite, version control discipline, a spec). Leave it empty rather than inventing a plausible prerequisite the sources do not state
    - failureMode states how the practice typically goes wrong in the sources' own accounts, not hypothetical risks. Leave it empty when no source reports a failure
    - evidenceOrigin names what kind of evidence supports the practice — one practitioner's account, a vendor's own documentation, a controlled study, a survey — not how strong it is. When the only evidence is a single practitioner's experience or a vendor describing its own product, say exactly that; never let a single source's recommendation read as established practice
    - tool lists the software the practice is commonly carried out with. WikiLink each tool that has its own [[SoftwareApplication/slug]] page and write the others as plain text. Leave it empty for a practice that is tool-independent
    - Notes is optional and holds only what cannot be said inside the four sections above: an observation that becomes visible only by placing several sources side by side (a convergence, a disagreement, a tension between what one source claims and what another ships), or a question none of the sources answers. Write each one with explicit attribution to what makes it visible — "across these accounts", "no source describes" — so a reviewer can check it against the material rather than against their own agreement. A restatement of a single source belongs in the body or in Evidence, not here. Never write normative advice ("you should", "start with") — this page reports what the sources support, and a recommendation the sources do not make is the one thing that cannot be traced. Omit the section entirely when nothing survives these rules; an invented insight costs more than an absent one
    - When several sources describe materially different versions of the same practice, present them side by side rather than treating the most detailed or most familiar one as the baseline (same rule as DefinedTerm.md)
title: ""
type: "schema:custom/Practice"
lang: ""
sources: []
tags: []

properties:
  description: ""
  appliesWhen: ""
  precondition: ""
  failureMode: ""
  evidenceOrigin: ""
  tool: []
---

(One paragraph: what this practice is and what problem doing it solves)

## When to Apply
(the situations where it pays off, and the situations where the sources say it does not)

## How It Works
(the shape of the practice — what the practitioner actually does, at a level a reader can act on without this becoming a step-by-step procedure)

## Failure Modes
(how it goes wrong in the sources' accounts, and what the sources say about avoiding that)

## Evidence
(who reports this working, and on what basis — experience, vendor documentation, measurement)

## Notes
(optional: what only becomes visible across several sources, and what none of them answers — omit the section when there is nothing)
