---
wikicommit:
  base: https://schema.org/CreativeWorkSeries
  provenance: generate-interactive
  granularity:
    - Create a page for a named, ordered collection of published works that is treated as a single titled whole by its own publisher — a guide made of numbered chapters, a book series, a named article series. The collection must have a title of its own that the source uses, not merely a tag or topic under which several pieces happen to sit
    - "Record the constituent works in hasPart only where this wiki has taken in a source for them; a chapter list copied out of the collection's own table of contents is navigation, not knowledge, and produces WikiLinks to pages nothing will ever write (Issue #570's thin-source concern applies with full force to an index page, whose extracted text is almost entirely link text)"
    - Prefer schema:Book when the collection has a fixed publication date, a stable set of parts, and does not change after publication — a series is for a collection still being added to
    - Prefer schema:BlogPosting for the individual dated post that announces or discusses a series; the announcement and the series are two entities, and the post is the one with a fixed date and author
    - Boundary — a CreativeWorkSeries is the container, never its contents. A single chapter, post, or article within the collection is not a series, and does not get a page of this type even when it is the only part this wiki covers. It is also not a publisher, a website, or a body of work grouped only by subject matter
title: ""
type: "schema:CreativeWorkSeries"
lang: ""
sources: []
tags: []

properties:
  about: ""
  author: ""
  url: ""
  startDate: ""
  creativeWorkStatus: ""
  hasPart: []
---

(2-3 paragraph overview of the series: what it collects, who produces it, and what
distinguishes it from a one-off work)

## Scope & Structure
(how the collection is organized, and how its parts relate to one another)

## Status
(whether the series is complete or still being added to, and what that means for a reader)
