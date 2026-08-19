---
wikicommit:
  base: https://schema.org/PresentationDigitalDocument
  provenance: generate-interactive
  granularity:
    - Create a new page for a specific, named slide deck or talk presentation published as its own citable artifact — a conference talk deck, a meetup presentation, a published keynote
    - A talk mentioned only as a passing citation, or named only to date an event, is an incidental mention, not an independent subject — do not create a page for it
    - The body should summarize the argument the presentation makes and the structure it uses to make it, not transcribe every slide
    - Prefer extracting the concepts, practices, or tools a presentation describes as their own pages (e.g. DefinedTerm, SoftwareApplication) over creating a page for the presentation itself, unless its identity as a specific talk (who gave it, where, when) is itself relevant to the wiki's theme
    - Slide decks are terse and heavily abbreviated by nature; state only what the slides actually assert, and do not reconstruct the speaker's unwritten narration into claims the deck does not make
    - author names the presenter; link them with a WikiLink to [[Person/slug]] when they independently qualify for their own page, and write the name as plain text otherwise
    - recordedAt names the conference or event the presentation was given at; link it with a WikiLink to [[Event/slug]] when the event independently qualifies for its own page, and mention it in body prose otherwise
    - Boundary with TechArticle/BlogPosting: a written article or post is not a presentation even when it covers the same talk; use this type only for the slide deck or talk artifact itself
    - Boundary with Event: the conference or meetup is an [[Event/slug]]; this page is the single presentation given there
title: ""
type: "schema:PresentationDigitalDocument"
lang: ""
sources: []
tags: []

properties:
  description: ""
  author: "[[Person/slug]]"
  datePublished: ""
  recordedAt: "[[Event/slug]]"
  url: ""
---

(2-3 paragraph overview: what the presentation argues, who gave it and where, and its significance)

## Key Points
(the presentation's central argument, framework, or recommendations, in list or prose form)

## Context
(the event and audience it was given to; how it relates to other work on the same topic; the speaker's stated perspective or caveats)
