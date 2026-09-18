---
title: "Six-Dimension Process Taxonomy"
type: "schema:DefinedTerm"
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
  description: "A comparative instrument for frameworks that add process to AI coding agents, scoring each on six dimensions — specification, context, roles, execution, validation and portability — against a three-point rubric."
---

The six-dimension process taxonomy is an instrument proposed in
[[ScholarlyArticle/from-prompt-to-process]] for comparing frameworks that run over an AI coding agent
to organise the work around it. It is offered as a replicable instrument rather than a descriptive
vocabulary: each dimension carries a guiding question and a set of observable indicators, and a
three-point rubric scores a framework 0 where the dimension is absent or incipient, 1 where it is
partial, and 2 where it is strong or central to the design.

## Usage

The six dimensions, with the question each asks:

- **Specification** — how does intention become a work contract? Indicators are specs, PRDs, plans,
  stories, tasks and acceptance criteria. Its weak extreme is a bare prompt; its strong extreme is a
  versioned set of requirements, acceptance criteria, plans, tasks, architecture and policies.
- **Context** — how does the agent know what is relevant? Indicators are the repository, documentation,
  hooks, rules, memory, evidence and gaps. This dimension covers what the framework decides the agent
  should know before acting.
- **Roles** — who decides, who implements and who reviews? Indicators are personas, agents, skills,
  responsibilities and authority. Role division is meant to reduce prompt ambiguity and create output
  expectations.
- **Execution** — does the framework act on the environment or only guide? Indicators are code editing,
  commands, tests, browser, terminal and IDE.
- **Validation** — how are errors detected before they become deliverables? Indicators are tests,
  checklists, gates, artifacts, human review and confidence labels.
- **Portability** — does the process survive outside one tool? Indicators are multiple integrations,
  open formats, lock-in and local installation.

The dimensions are explicitly treated as complementary reading lenses rather than disjoint partitions,
so a single feature may score in more than one: the paper's own example is that isolating
implementation in git worktrees is execution, while requiring review and acceptance before the merge is
validation, and one framework's worktree design does both.

Applied to six frameworks, the instrument produced no score of 2 across all six dimensions. The pattern
the author reads out of the resulting table is a structural opposition between process depth and
portability: the two frameworks scoring 2 on portability sacrifice roles and validation, the framework
with the deepest process total reduces portability and execution, and the one most focused on context
scores zero on roles, validation and portability. Specification, scoring 2 for almost every framework,
is identified as the field's common denominator and therefore the dimension that discriminates least;
roles and validation, being the most polarised, discriminate most.

## When It Applies

The instrument applies to what the paper calls support frameworks — a layer of artifacts, commands,
roles, templates, workflows or policies running over a development agent someone already operates. It
does not apply to the agents or runtimes themselves, to closed IDEs and platforms that embed an agent,
or to general-purpose SDKs for building agent systems; all three were excluded by category from the
study that proposes it.

It assumes that the framework's official documentation and repository are a sufficient basis for
scoring, since most of the frameworks it was built for have not been through independent academic
evaluation. That assumption is also its main weakness as applied: the scores reported with it express
the author's judgement from that documentation rather than a third-party-validated empirical
measurement, and the paper records that the scoring was done by a single rater with no second
independent coder and no inter-rater reliability reported.

One demonstrated property is worth separating from the scores themselves. Applying the instrument to a
framework deliberately excluded from the sample for low traction yielded the most complete profile of
any case examined, which the paper reads as evidence both that the taxonomy generalises beyond its
sample and that adoption and process completeness are orthogonal dimensions — so a traction filter
selects for the most adopted frameworks, not the most complete ones. Scores are also a snapshot: the
frameworks they describe are under active development and the underlying traction figures are dated to
May 2026 in the source.

As a scheme it is new and rests on a single self-contained study. The author presents it as the
paper's central contribution and states that the six dimensions were chosen because they recur, under
different names, across the six frameworks analysed, rather than being derived from prior theory.

## Related Terms

- [[ScholarlyArticle/from-prompt-to-process]] — the study that proposes this taxonomy and applies it
- [[DefinedTerm/spec-driven-development]] — the practice most of the scored frameworks implement, and
  the source of the specification dimension's strong extreme
- [[DefinedTerm/reverse-documentation-engineering]] — the inverse direction one scored framework takes,
  recovering specifications from existing systems rather than writing them for new ones
- [[DefinedTerm/context-engineering]] — the concern the context dimension measures
