---
wikicommit:
  base: https://schema.org/Report
  provenance: generate-interactive
  granularity:
    - Create a new page for a specific, named report or whitepaper published by an organization as its own citable artifact — an industry trends report, a survey report, a research or assurance report, a government report
    - A report mentioned only as a passing citation, or cited only for a single statistic with no discussion of the report itself, is an incidental mention, not an independent subject — do not create a page for it
    - The body should summarize what the report claims, predicts, or found, and the evidence base it rests on, not reproduce its full contents
    - Prefer extracting the concepts, practices, or tools a report describes as their own pages (e.g. DefinedTerm, SoftwareApplication) over creating a page for the report itself, unless the report's identity as a specific, citable publication (who published it, as of when) is itself relevant to the wiki's theme
    - author lists named authors when the report credits any; link each author who independently qualifies for their own [[Person/slug]] page with a WikiLink, and list others as plain text. Organizational reports often credit no individual author — leave it empty rather than substituting the publishing organization
    - publisher names the publishing organization; link it with a WikiLink to [[Organization/slug]] when it independently qualifies for its own page, and write it as plain text otherwise
    - A report published by a vendor about its own products is still a Report, but state its predictions and figures as that vendor's own claims rather than as established fact
    - Boundary with ScholarlyArticle: a peer-reviewed or preprint academic work with an abstract and citations is ScholarlyArticle even when it is titled a "report"
    - Boundary with TechArticle: a document whose purpose is to specify how something is done (procedures, configuration, best practices) is TechArticle; a Report presents findings, predictions, or an assessment
    - Boundary with NewsArticle/BlogPosting: journalistic reporting *about* a report is a NewsArticle, and a blog post summarizing one is a BlogPosting — neither is the report itself
title: ""
type: "schema:Report"
lang: ""
sources: []
tags: []

properties:
  description: ""
  author: []
  publisher: "[[Organization/slug]]"
  datePublished: ""
  abstract: ""
  reportNumber: ""
---

(2-3 paragraph overview: what the report covers, who published it, and its main findings or predictions)

## Key Findings
(the report's central claims, predictions, or figures, in list or prose form)

## Basis & Caveats
(what evidence the report rests on — surveys, internal research, customer observations — and the limitations or hedges it states about its own conclusions)
