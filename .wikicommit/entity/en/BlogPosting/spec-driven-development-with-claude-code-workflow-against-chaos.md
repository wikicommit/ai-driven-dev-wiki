---
title: "Spec-Driven Development mit Claude Code: Workflow gegen Chaos"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, coding-agents]
sources:
  - type: url
    url: 'https://florian-gahn.de/blog/spec-driven-development-claude-code'
    hash: sha256:c279384471d8164225c592ecf6b9fc84ab7375d80a8d67e843dfe89be59ec75e
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A German-language blog post by Florian Gahn that explains spec-driven development, in which the specification rather than the code is the primary artifact, and how to practise it with Claude Code. It surveys the 2026 tool landscape, weighs practitioner reports for and against the approach, and proposes a three-step pilot setup."
  author: ["Florian Gahn"]
---

This German-language post on Florian Gahn's blog introduces
[[DefinedTerm/spec-driven-development]] (SDD) as an approach that makes the specification the
primary artifact of software development. Code is generated from it, and the spec remains the
source of truth. The post names GitHub Spec Kit ([[SoftwareApplication/github-spec-kit]]),
Amazon's [[SoftwareApplication/kiro]] and the Tessl Framework ([[SoftwareApplication/tessl]])
as drivers of the trend in 2026. It describes a concrete workflow with
[[SoftwareApplication/claude-code]] and compares the main tools. It then sets out when the
approach pays off, what its risks are, and how to start.

The post presents SDD as a discipline with clear strengths and equally clear breaking points,
rather than as hype, and calls it the honest answer to [[DefinedTerm/vibe-coding]]. It draws on
named practitioners on both sides: a large ERP modernisation as a success story, and a
Thoughtworks expert's critique of the "Markdown hell" the tools produce. The post states at its
end that it was written with AI support and editorially checked.

## Key Points

- In SDD the specification, not the code, is the primary source document. AI generates tests,
  plans and implementation from it, and the developer verifies each step before moving on.
- The term is not new: the post traces an "agile specification-driven development" approach
  back to 2004. What it says is new is that AI agents make the approach practical without
  custom code generators.
- The post adopts a three-level distinction between spec-first, spec-anchored and
  spec-as-source ([[DefinedTerm/spec-driven-development-levels]]), which it attributes to
  Thoughtworks' Birgitta Böckeler. It says only the Tessl Framework currently pursues
  spec-as-source consistently, and that most tools deliver spec-first while claiming to be
  spec-anchored.
- It presents SDD as a structural response to AI generating code faster than people can
  understand it. It adds regulatory pressure as a second driver: EU AI Act Article 14 requires
  effective human oversight of high-risk AI systems, which the post dates to 2 August 2026
  unless the date is postponed.
- Claude Code's Plan Mode is described as a lightweight, built-in form of SDD. In this mode
  Claude reads code, researches context and proposes a plan without writing anything, and
  switches to editing only after approval. The post cites Anthropic's recommended four-phase
  workflow, Explore → Plan → Implement → Commit.
- A documented workflow by an AWS solutions architect anchors a project in three Markdown
  files: a running [[DefinedTerm/claude-md]] steering document, a central specification file
  written before any code, and a SKILL.md capturing reusable building blocks at the end. Work
  is split into small, testable phases instead of a single "build the whole thing" prompt.
- Spec Kit is installed as the `specify` CLI and used through slash commands for specify, plan
  and tasks. It adds a "constitution" of immutable project principles that is read in at every
  step. Kiro uses three files and three phases, with user stories and acceptance criteria in
  [[DefinedTerm/easy-approach-to-requirements-syntax]] (EARS) notation.
- The tool comparison also covers Aider's architect mode, where one model plans and another
  edits, and which the post says is not classic SDD. It covers [[SoftwareApplication/cursor]]
  project rules and [[DefinedTerm/agents-md]] as a low-threshold spec-anchored entry point,
  [[SoftwareApplication/bmad]] as a popular but restrictive method framework, and knowis AG's
  commercial Cloud Solution Workbench.
- According to the post, SDD pays off when code goes to production, has to be understood by
  several people, and rests on sufficiently clear requirements. Regulated industries, legacy
  modernisation and teams with distributed responsibility are its typical fields. It is
  unsuitable for prototypes, very small bugs and highly exploratory work.
- The post names three risks: a "Markdown hell" of files to review; a false sense of control,
  since the AI still does not reliably follow the specs; and a parallel with the failed
  model-driven development of the 2000s. The worst case it describes combines MDD's
  inflexibility with LLM non-determinism.
- For a pilot it recommends choosing one bounded feature, keeping tooling minimal, and adding a
  "comprehension gate" in which a human must be able to explain the AI's chosen solution before
  each merge.

## Context

The post frames SDD as the professional answer to the scaling limits of vibe coding, while
stressing that the tools are young, reviews are laborious and the risk of making things worse
is real. It notes that a roughly 30 percent productivity figure it cites comes from vendor
material, and that robust studies on the return on investment are still missing. Its final
advice is to pilot with Spec Kit or Kiro, add comprehension gates, and measure honestly whether
the stacks of Markdown actually improve output.
