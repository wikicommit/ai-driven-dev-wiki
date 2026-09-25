---
title: "Spec-first, spec-anchored and spec-as-source"
type: "schema:DefinedTerm"
lang: en
tags: [spec-driven-development]
aliases: ["Spec-first", "Spec-anchored", "Spec-as-source", "SDD implementation levels"]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html'
    hash: sha256:a502c8234d3e0bd54bf8eec4d887723cc3b3872d1015d79b4f4c6143f2498f7b
  - type: url
    url: 'https://www.cnblogs.com/studyzy/p/19638317'
    hash: sha256:105218db5ca2d8c9d618572ca661b03b7775fd1a43df1b7ac3e8137ff20f5f78
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Three implementation levels of spec-driven development proposed by Birgitta Böckeler in October 2025: a spec written first for the task at hand, a spec kept and evolved for the feature afterwards, and a spec that is the main source file which humans edit instead of the code. A later Chinese-language post uses the same three names for schools of SDD distinguished by how the spec relates to the code."
---

Spec-first, spec-anchored and spec-as-source are three implementation levels of
[[DefinedTerm/spec-driven-development]] that Birgitta Böckeler proposed in
[[BlogPosting/understanding-spec-driven-development-kiro-spec-kit-and-tessl]], after looking at how the
term was used and at tools that claim to implement it. In **spec-first**, a well thought-out spec is
written first and then used in the AI-assisted development workflow for the task at hand. In
**spec-anchored**, the spec is kept after the task is complete and used for the evolution and
maintenance of that feature. In **spec-as-source**, the spec is the main source file over time: only
the spec is edited by the human, who never touches the code. She presents the levels as building on
one another.

## Usage

In the article's diagram of the levels, a spec-first spec is deleted once the feature is created and a
new spec describing each later change is written, while a spec-anchored spec is instead edited as the
feature evolves. The author observes that every SDD approach and definition she found is spec-first,
but not all strive to be spec-anchored or spec-as-source, and that the strategy for maintaining specs
over time is often vague or left open. Applying the levels to three tools, she reads
[[SoftwareApplication/kiro]] as mostly spec-first; [[SoftwareApplication/github-spec-kit]] as still
spec-first only, despite GitHub's stated aspiration to spec-anchoring, because it creates a branch per
spec; and [[SoftwareApplication/tessl]] as the only one explicitly aiming for spec-anchored and
exploring spec-as-source.

### As three schools

A Chinese-language post on the 深蓝居 blog (February 2026) uses the same three names for three schools
of SDD that differ in how they position the spec relative to the code, and treats them as options to
choose between rather than as levels. In its account, the **spec-as-source** ("radical") school treats
code as an intermediate product between spec and binary: only the spec is maintained, code can be
discarded and regenerated, and manual edits to generated code must be fed back into the spec. It
places this school in systems with extreme consistency requirements such as financial cores, telecom
protocols and cryptographic algorithms. **Spec-anchored development** ("traditional") keeps the spec as
an anchor with two-way synchronization — spec changes drive code updates and code improvements may
update the spec — while humans keep control of core business logic; the post sees it as fitting most
enterprise applications. **Spec-first** ("lightweight") treats the spec as a "super prompt" at the
start of development: a lightweight spec such as a Markdown checklist guides AI generation, and the
spec is then archived as a decision record without enforced synchronization, so its authority fades
over time. The post places it in rapid prototyping, exploratory work and small internal tools, and
argues that mature teams mix all three — spec-as-source for core modules, spec-anchored for business
modules and spec-first for tool scripts.

## When It Applies

The levels are a descriptive classification from one author's review of the term's usage and three
tools as of late 2025, not an established standard. She regards the spec-first principle as valuable
in many situations. For spec-as-source in particular she draws a parallel with model-driven
development, which never took off for business applications, and wonders whether spec-as-source, and
even spec-anchoring, might end up with the downsides of both model-driven development and LLMs:
inflexibility and non-determinism. The later post's school-by-context guidance is likewise one
author's recommendation rather than a measured result.

## Related Terms

- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/memory-bank]]
- [[DefinedTerm/sdd-five-layer-execution-model]]
