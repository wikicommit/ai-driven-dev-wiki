---
wikicommit:
  base: https://schema.org/TechArticle
  provenance: collect
  granularity:
    - Create a new page for a technical document that specifies a procedure, configuration, or set of practices as its own citable artifact — official product documentation, vendor engineering guides, and practitioner write-ups of a named technique all qualify
    - A document mentioned only as a passing citation is not an independent subject — do not create a page for it
    - The body should summarize what the document prescribes and the conditions it applies under, not reproduce its instructions verbatim
    - Prefer extracting the techniques, terms, or workflows a document describes as their own pages (e.g. DefinedTerm, HowTo, SoftwareApplication) over creating a page for the document itself, unless the document's identity as a specific, citable reference (who publishes it, for which tool, as of when) is itself relevant to the wiki's theme
    - author lists multiple names; link each author who independently qualifies for their own [[Person/slug]] page with a WikiLink, and list others as plain text. Official documentation often has no named author — leave it empty rather than substituting the publishing organization
    - publisher names the publishing organization; link it with a WikiLink to [[Organization/slug]] when it independently qualifies for its own page, and write it as plain text otherwise
    - Boundary with BlogPosting: a TechArticle's purpose is to specify how something is done (procedures, configuration, best practices, specifications); a BlogPosting argues a position or recounts an experience. Official docs and engineering handbooks are TechArticle even when hosted on a blog path; an opinion piece is BlogPosting even when technical
    - Boundary with HowTo: HowTo is for a self-contained ordered sequence of steps toward one outcome. Use TechArticle for a reference document that states practices, rationale, and configuration without being reducible to a single step sequence
    - Boundary with ScholarlyArticle: a peer-reviewed or preprint academic work is ScholarlyArticle even when its subject is a technique
title: ""
type: "schema:TechArticle"
lang: ""
sources: []
tags: []

properties:
  description: ""
  author: []
  datePublished: ""
  publisher: ""
  proficiencyLevel: ""
---

(2-3 paragraph overview: what the document specifies, who publishes it, and which tool or practice it governs)

## Key Practices
(the practices, procedures, or configuration the document prescribes)

## Scope & Caveats
(the conditions and versions it applies to; stated limitations, prerequisites, and how it relates to adjacent documentation)
