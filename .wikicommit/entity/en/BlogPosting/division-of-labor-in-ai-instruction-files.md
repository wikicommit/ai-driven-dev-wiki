---
title: "AIに渡す指示書の役割分担: AGENTS.md/SKILL.md/DESIGN.mdと仕様駆動開発の現在地"
type: "schema:BlogPosting"
lang: en
tags: [agent-config, spec-driven-development, design-systems]
sources:
  - type: url
    url: 'https://zenn.dev/genda_jp/articles/f71d3ed7d4d7e8'
    hash: sha256:3b930434d815794b112529193eb4b0eb5224288334a07ea828aa21c4e620cc28
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A post arguing that the instruction files given to AI coding agents have split into three layers with non-overlapping concerns — AGENTS.md for an agent's premises, SKILL.md for reusable tasks, DESIGN.md for design-system specifications — and setting that split against spec-driven development."
  author: "ikenyal"
  datePublished: "2026-05-03"
  publisher: "GENDA"
---

This post reads the instruction files handed to AI coding agents as having separated into three
layers that do not overlap: [[DefinedTerm/agents-md]] (and its tool-specific equivalent `CLAUDE.md`)
for an agent's overall premises, roles and prohibitions; `SKILL.md` for reusable individual tasks;
and [[DefinedTerm/design-md]] for design-system specifications. Its occasion is the third of these
arriving — Google Labs published the `DESIGN.md` specification in April 2026 — which the author
takes as completing a set rather than adding a competitor.

The argument the post builds on that observation is about where each layer places the balance between
machine-readable and human-readable content, and it offers the three-way split as a practical
criterion for breaking up a single overloaded `CLAUDE.md`. Its second half sets the three layers
against [[DefinedTerm/spec-driven-development]], finding a shared philosophy but a different time
axis.

The post is written from the author's own operation of an instruction-file repository, and it is
explicit that the three-layer split is an option to adopt where it earns its place rather than a
target state.

## Key Points

- The three file formats divide by subject rather than compete: `AGENTS.md` covers an agent's
  premises and boundaries, `SKILL.md` a reusable unit of task execution, and `DESIGN.md` the
  appearance a generated UI should have. The post states that what each covers does not overlap.
- Where each format sits on the machine-readable/human-readable axis differs by layer, and the post
  presents that as the substance of the split: `AGENTS.md` is almost entirely human-readable prose
  because conveying context and nuance is what it is for; `SKILL.md` structures only its leading YAML;
  `DESIGN.md` separates the two explicitly, with machine-readable design tokens in the front matter
  and human-readable design intent in the body.
- The post offers three questions as a way to decide whether to split an existing `CLAUDE.md`: does it
  contain design-system conventions (move them to `DESIGN.md`), does it contain specific task
  procedures (move them to `SKILL.md`), and what remains is the agent's premises and boundaries,
  which is the `AGENTS.md` layer.
- Spec-driven development and the three-layer split share several commitments in the author's
  reading — writing before implementing, holding machine-readable and human-readable content
  together, keeping persistent context for the AI to consult each time, and fixing decisions in a
  known place — but differ on time axis: an SDD spec describes what is about to be built and is
  archived once the feature is done, while the three-layer files describe standing norms that are
  maintained and grow.
- The author argues that not everything should be specified. The criterion offered is whether a rule
  is formally verifiable: a contrast ratio or a term substitution is, a document's tone or overall
  stance is not, and the latter is said to lose its substance if forced into a specification.
- The post reports that the two communities had not yet substantially intersected as of May 2026 —
  SDD discussion concentrating on how to build a feature, three-layer discussion on how to hand over
  norms — and suggests the natural connection is a feature spec referencing a persistent
  `DESIGN.md` token. It states that this is not yet a widely established practice.

## Context

The post's framing of the problem is that unstructured natural-language instruction documents mix
two kinds of rule: ones that are formally checkable and ones that require judgement. Because both sit
in the same file, the checkable ones end up relying on human review as well. The three formats are
presented as an answer to that specific mixing.

Where the post's claims rest on the author's own operation of an instruction-file repository — a
writing style guide of about 150 lines, and around fifteen role-specific instruction files — it says
so, and those passages are one practitioner's account rather than a surveyed practice. Its
descriptions of what each format is for are drawn from the projects that publish them.
