---
title: "Agentic Engineering Is Just Everything We Haven't Been Doing"
type: "schema:BlogPosting"
lang: en
tags: [agentic-engineering, engineering-practice, organizational-change]
sources:
  - type: url
    url: 'https://blog.matthewbrunelle.com/agentic-engineering-is-just-everything-we-havent-been-doing/'
    hash: sha256:a57c3f89f2c2b54dd0f3a7abd19439524919c3c76a1c07c94e04bb4f203ce639
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A post by Matthew Brunelle arguing that the practices people adopt to make agentic engineering work are the ordinary software engineering practices teams have long cut under time pressure, and that a dysfunctional engineering organisation will find agentic engineering correspondingly harder."
  author: "Matthew Brunelle"
  datePublished: "2026-08-12"
  publisher: ""
---

This post argues that the enthusiasm around improving agentic engineering is mostly enthusiasm for practices software engineers should already have had in place — "the kind of work we typically cut because of time pressure." Its worked example is using an issue tracker to record requirements so work can be handed to an agent that comments with questions and updates status, which the author points out is just normal software engineering.

The author states his own framing up front: the post is not advocating for adopting agentic engineering, but is written on the assumption that the reader has chosen to try it or had that decision made for them. He notes the views are his own.

## Key Points

- **The practice list is unremarkable on purpose.** Docstrings on methods, descriptive pull requests, keeping documentation current or writing it at all, meaningful tests or any tests, automated linting or even agreed code conventions, planning and getting design feedback before implementing, capturing meeting notes and confirming what was decided, and holding conversations in open searchable channels rather than DMs.
- **The author's reaction is mixed rather than celebratory**: relief that people are excited to do these things now, disappointment that it took agentic engineering to prompt it, and the question "why are we holding the bots to higher standards than ourselves?"
- **Documentation gains force when agents read it.** A coworker is quoted describing how a review revealed missing guiding principles, and how encoding them in documentation now works where it previously would not — because before, having an effect would have required a conversation with the whole team to memorise them, whereas now every engineer's agent reads and adheres to the documentation.
- **A limit drawn from James C. Scott's mētis.** The post cites *Seeing Like a State* for the idea of knowledge acquired only by long practice at similar but rarely identical tasks, where knowing how and when to apply rules of thumb in a concrete situation is the essence. Its application is that code syntax is a well-described human construct and safe to automate, while other engineering principles are free-form and harder to make legible — "a written rule is not a judgment" — though it concedes a frozen legible system beats nothing at all.
- **The stated thesis and its corollary**: if "agentic engineering is just normal engineering with robots," then "anything that makes engineering harder makes agentic engineering much harder," because agents lack the mētis to navigate a situation the way a person would. Its illustration is a friend who had to discard agent output after a team changed one of his dependencies mid-sprint without communicating.
- **The closing advice is diagnostic.** If agentic engineering is going badly, check whether ordinary software engineering is also hard at that company: "slapping AI on a dysfunctional system, be it people or software, will not fix your problems." The post ends by invoking the long-known result that adding people to a late project makes it later, and adds that "adding a fake person is no better."

## Context

This is a short opinion post rather than a study, and it says so — its evidence is the author's own observation, one quoted coworker, and one quoted friend. Its value is as a statement of the deflationary position on [[DefinedTerm/agentic-engineering]]: that the discipline being described as new is a re-encounter with existing practice under new pressure, which is a claim about framing rather than one that can be settled by measurement.
