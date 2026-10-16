---
title: "仕様書駆動開発の課題をチームで改善した3つの工夫"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, code-review, multi-repository, team-practices]
sources:
  - type: url
    url: 'https://zenn.dev/hacobell_dev/articles/67b258c7ee4cd0'
    hash: sha256:8fe042ec42fe7df7c0aa22d2cbac0a0e88cca59ca6fa93b5f37742aef40f3cae
review_status: pending
generated_at: "2026-10-16"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.10.0"

properties:
  description: "A December 2025 Japanese-language post on the Hacobell Developers Blog describing two problems a team met in about three months of practicing spec-driven development with AI agents — heavy spec review and design across multiple repositories — and three countermeasures it adopted: a key-points summary document, a submodule-based integration repository, and daily mob sessions."
  author: ["meimei"]
  datePublished: "2025-12-22"
  publisher: "Hacobell Developers Blog"
---

This Japanese-language post, written for the Hacobell Developers Advent Calendar 2025, reports on roughly three
months of a team's experience with [[DefinedTerm/spec-driven-development]] (SDD), which the post describes as
writing specifications before code and developing from them. The team adopted it because documenting
requirements and design in detail, and discussing and agreeing on them as a team, was expected to make team
development with AI agents easier.

The author credits SDD with aligning the team before development starts and with letting the AI agent act as
the "driver" on complex, uncertain implementations while the humans concentrate on discussion. The post then
describes two problems the team ran into and three practices it introduced to address them.

## Key Points

- The first problem the post names is review load: because SDD produces detailed documents, the specs became
  very large and took a long time to review. The author notes that the author of the SDD tool
  [[SoftwareApplication/cc-sdd]] has raised the same point and suggests many SDD users likely share it.
- The second problem was multi-system design: the team manages several systems in a multi-repository layout, and
  specs generated within one repository could not take the other systems' code into account; supplying that
  knowledge or pointing at the relevant repositories each time was possible but laborious.
- The first countermeasure was to generate a file extracting the key points of the requirements and design
  documents and to make reviewing that summary file the minimum required. The author acknowledges that reviewing
  every spec is the ideal, but argues that a review load too heavy to let development proceed lowers
  productivity; the summary also collects the points the team wants to discuss.
- The second countermeasure was an integration repository that includes every repository as a git submodule. It
  holds shared requirements, inter-system interface definitions and domain knowledge (ubiquitous language), while
  each service repository holds its own design, summary and task documents; each repository refers back to the
  integration repository through symbolic links set up in a way every team member uses.
- According to the post, the integration repository let generated designs take every repository's code into
  account, improved the quality of the design documents generated in each repository, and ended the duplication
  of similar requirements documents across repositories, which in turn also reduced review load.
- The third countermeasure was a daily one-hour mob session. The author explains that members have different
  amounts of time for review and that asynchronous review of long specs let important points slip and delayed
  reviews; in the session the whole team reviews the summary document together after a spec is written, checks
  that the overall design is sound, and discusses open points. Mob programming is sometimes done there for highly
  complex implementations, and the session doubles as a place for questions.
- The author reports that more time working and discussing as a whole team has prevented large divergences in
  direction and lets open points be resolved quickly; these are the team's own observations rather than measured
  results.

## Context

The post closes by noting a discussion that development in the AI era may require changing the process itself
substantially from conventional Scrum, and says the team intends to keep exploring a better form of SDD for
itself. It is a firsthand account from one team's practice, not a general evaluation of the method.
