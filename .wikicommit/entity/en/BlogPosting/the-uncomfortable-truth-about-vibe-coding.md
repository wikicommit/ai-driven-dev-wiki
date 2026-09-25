---
title: "The uncomfortable truth about vibe coding"
type: "schema:BlogPosting"
lang: en
tags: [vibe-coding, spec-driven-development, ai-assisted-programming]
sources:
  - type: url
    url: 'https://developers.redhat.com/articles/2026/02/17/uncomfortable-truth-about-vibe-coding'
    hash: sha256:42f3249cb6e39d9ef4f8c213fa9e954e331b6f259c1af55afe2c58acef2f03fb
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A February 2026 article on Red Hat Developer arguing that vibe coding is fast and useful for prototypes but that projects built without specifications hit a wall as they grow, and recommending spec-driven development for anything that must be maintained, with vibe coding kept for exploration and for units small enough to test."
  author: "Todd Wardzinski"
  publisher: "Red Hat"
  datePublished: "2026-02-17"
---

*The uncomfortable truth about vibe coding*, published on Red Hat Developer on 17 February 2026, is a
practitioner's argument that [[DefinedTerm/vibe-coding]] is at once the most exciting and the most
dangerous development practice to emerge in years. The author defines vibe coding broadly, as building
software by conversing with AI rather than writing every line yourself, and writes from personal
experience, reporting having brought five concepts to life and created three minimum viable products
in a few months, with projects that would once have taken quarters of evenings now taking weekends.

The article's case is that this speed holds for straightforward, self-contained projects and breaks
down as a project grows, and that the remedy is not to abandon vibe coding but to move to
[[DefinedTerm/spec-driven-development]] once the prototyping phase is over.

## Key Points

- The author accepts that vibe coding works for certain things — a quick prototype, a flashcard app, a
  landing page — and argues that natural language suits how people think, letting a developer focus on
  what they are building rather than how.
- The author describes a failure pattern in which, a few months into a project, changing one small thing
  breaks several other features and each fix breaks something else — "whack-a-mole" with one's own
  code base — and says many vibe-coded projects hit a wall around the three-month mark.
- The author attributes this not to the AI being unintelligent but to building without specifications: the
  instructions become obsolete the moment code is generated, the code becomes the only source of truth
  for what the software does, and code is poor at explaining why it does it, so the intent behind
  decisions is lost and the code base outgrows what anyone, including the AI's context window, can hold.
- Spec-driven development is presented as the reversal of that relationship: specifications become the
  authoritative, version-controlled blueprint the code must conform to, and when something breaks the
  developer refines the spec and regenerates rather than editing the code. The author concedes this is
  extra work at first and argues it pays back in documentation that stays current, collaboration at the
  spec level, and changes made in one place.
- The author argues that developers still need to be technical — to understand architecture, dependencies,
  constraints and trade-offs — because a specification written without that understanding is "a wish
  list", and compares the shift to the move from assembly to high-level languages, where the
  abstraction changed but the need for competence did not.
- The article's rule for where vibe coding still belongs inside a spec-driven workflow is the unit level: if a
  unit or functional test can validate the output, the scope is small enough to vibe; if not, it needs
  a spec. The author presents this as what keeps a project out of the whack-a-mole trap, because each piece can
  be verified in isolation before it joins the larger system.
- The article names Amazon's [[SoftwareApplication/kiro]], GitHub's [[SoftwareApplication/github-spec-kit]],
  Codeplain and [[SoftwareApplication/tessl]] as tools emerging to bridge vibing and building, and
  describes GitHub's research arm as having explored the territory in 2023 with an experimental
  project, SpecLang, that used structured natural language to generate code and never shipped as a
  product.

## Context

The article is one practitioner's argument, grounded in the author's own projects and in anecdotes, rather than a
measured study; the three-month figure is the author's observation, not a reported statistic. The article's prescription is a division of labour between the two
modes rather than a rejection of either: in its closing formulation, use the vibes to explore and use
specifications to build.
