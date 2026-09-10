---
wikicommit:
  base: https://schema.org/SoftwareApplication
  provenance: init-theme
  granularity:
    - Create a new page for any named software application, tool, IDE, CLI, extension, or hosted service treated as an independent subject
    - Use WikiLink [[SoftwareApplication/slug]] in body text for incidental mentions
    - Prefer schema:HowTo when the source's substance is an ordered set of steps the reader performs, even when those steps are performed with one named tool throughout. The workflow is the HowTo, and the tool it uses keeps its own page here
    - "Prefer schema:DefinedTerm when the subject is a methodology, practice, or piece of terminology rather than a shipping piece of software — vibe coding, spec-driven development, and agentic engineering are named practices, not applications, even where a single tool popularized one of them"
    - Prefer schema:Organization for the company, lab, or team that publishes a tool. The vendor and the product are separate subjects; link them through the author property rather than folding the vendor into the product page
    - A tool named only in passing as part of another subject's setup, tech stack, or list of alternatives, with no independent facts about the tool stated in the source, is an incidental mention, not an independent subject; do not create a page for it
    - "Record softwareVersion only when the source states a version and a claim on the page actually depends on it, and say which version each behavior was observed in. Tooling in this area changes fast, and an undated version number is a claim that quietly stops being true (this narrows what a page says, never whether it exists)"
    - Do not record pricing, plan tiers, download counts, or benchmark scores even when the source states them — they go stale between the source's publication and the reader's visit, and verifying them is out of scope for this wiki
    - Boundary — a SoftwareApplication is software someone runs. A specification, protocol, file format, API convention, or model weights release is not an application; use DefinedTerm for a concept or format, and reserve this type for something installable, invocable, or hosted
title: ""
type: "schema:SoftwareApplication"
lang: ""
sources: []
tags: []

properties:
  description: ""
  applicationCategory: ""
  operatingSystem: ""
  softwareVersion: ""
  featureList: ""
  author: "[[Organization/slug]]"
---

(2-3 paragraph overview of the application: what it is, who makes it, and what problem it addresses)

## Capabilities
(what the application does — its interface, notable features, and how it is invoked. Note the
version each behavior was observed in where the source states one)

## Adoption & Ecosystem
(how it is used in practice, what it integrates with, and the practices or workflows it is
associated with)
