---
wikicommit:
  base: https://schema.org/TechArticle
  provenance: collect
  granularity:
    - Create a new page only for a fixed-instance technical document — a whitepaper, practical guide, specification, or governance framework released as a discrete, dated report with an identifiable publisher or author
    - Do not create a page for a continuously-updated documentation page, API reference, or help-center article with no publication date of its own — that is a living resource, not a single-instance work, and the source-as-entity test excludes it; its content still informs the DefinedTerm/HowTo pages about the concepts it describes, it just does not get a page of its own
    - The body should summarize what the document itself recommends, specifies, or defines, not restate it verbatim
    - Prefer schema:HowTo when the source's substance is an ordered set of steps the reader performs, rather than a specification or set of recommendations
    - Boundary — a TechArticle is a technical document itself (a specification, whitepaper, or procedural/reference guide); use ScholarlyArticle when the document is peer-reviewed or preprint academic work, and use BlogPosting when it is an informal practitioner post rather than a formal published document
title: ""
type: "schema:TechArticle"
lang: ""
sources: []
tags: []

properties:
  description: ""
  author: []
  publisher: ""
  datePublished: ""
  proficiencyLevel: ""
  dependencies: ""
---

(2-3 paragraph overview: what the document is, who published it, and what it covers)

## Details
(the document's own recommendations, specifications, or definitions — not a restatement of unrelated background)
