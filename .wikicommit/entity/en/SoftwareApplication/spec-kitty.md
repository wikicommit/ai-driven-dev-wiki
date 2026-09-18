---
title: "Spec Kitty"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, spec-driven-development]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An open-source command-line tool for specification-driven development with code agents that keeps specifications, plans and tasks inside the repository and uses git worktrees to isolate implementation work behind review and acceptance gates."
  applicationCategory: "Spec-driven AI development toolkit"
  featureList: "spec / plan / tasks / next / review / accept / merge workflow; specifications, plans and tasks stored in a dedicated repository directory; git worktree isolation per work package; review and acceptance required before merge"
---

Spec Kitty is an open-source command-line tool for [[DefinedTerm/spec-driven-development]] with code
agents. It turns product requirements into repeatable workflows, keeping specifications, plans and
tasks inside the repository itself in a dedicated directory, and uses [[DefinedTerm/git-worktrees]] to
isolate the implementation work. Its declared flow follows the steps spec, plan, tasks, next, review,
accept and merge, and the framework announces support for multiple agents including Claude, Cursor and
Gemini. It is one of the six frameworks assessed in [[ScholarlyArticle/from-prompt-to-process]].

## Capabilities

The worktree isolation is what distinguishes Spec Kitty from the other specification-driven frameworks
in that assessment: agents implement work packages in a controlled way and the result passes through
review and acceptance before the merge. The study reads this as inserting human control points into the
flow and bringing it closer to established code-review practice, and uses it as its worked example of
why the taxonomy's dimensions overlap rather than partition — the worktrees isolate implementation,
which is execution, while requiring review and acceptance before the merge is validation, so the same
feature scores on both.

## Adoption & Ecosystem

Under the [[DefinedTerm/six-dimension-process-taxonomy]], Spec Kitty scores 2 on specification, 1 on
context, 1 on roles, 2 on execution, 2 on validation and 1 on portability — a total of 9 out of 12, the
second-highest of the six frameworks assessed and the only one scoring 2 on execution. Alongside
[[SoftwareApplication/bmad]], it is one of the two frameworks the study identifies as treating roles and
validation as central rather than leaving them weak, and one of the two it names as giving partial
answers to the tension between agent autonomy and governance by inserting human review points. The
scores express the study author's judgement from official documentation, not an independent empirical
measurement.

The caveat the study attaches is maturity: Spec Kitty was included at the threshold of the study's
traction filter, and the study describes its traction as still modest compared to the others, which
leaves its maturity and adoption open. Its portability is also qualified — although it works with multiple agents,
it depends on its own repository conventions and on git worktrees. The study additionally lists Spec
Kitty among the installable community frameworks that illustrate the emerging supply chain of commands,
skills, templates and workflows, and the supply-chain risk that comes with it.
