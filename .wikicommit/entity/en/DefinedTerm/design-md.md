---
title: "DESIGN.md"
type: "schema:DefinedTerm"
lang: en
tags: [agent-config, design-systems]
sources:
  - type: url
    url: 'https://zenn.dev/genda_jp/articles/f71d3ed7d4d7e8'
    hash: sha256:3b930434d815794b112529193eb4b0eb5224288334a07ea828aa21c4e620cc28
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A file format published by Google Labs in April 2026 for stating a design system in a form an AI agent can read: machine-readable design tokens in the leading YAML, human-readable design intent in the Markdown body, with a CLI that lints the result."
---

`DESIGN.md` is a file format for stating a design system so that an AI agent generating a user
interface has a fixed specification to work from. A single file holds both halves of that
specification: machine-readable design tokens — colours, typography, spacing, components — in a
leading YAML block, and the human-readable design intent behind them in the Markdown body beneath.
Google Labs published the format in April 2026, from a repository named `google-labs-code/design.md`,
as the reference implementation of its AI UI-generation product Google Stitch; the specification
document itself is published on the Stitch side.

## Usage

What distinguishes the format from a style guide is that it ships with a checker. A CLI invoked as
`npx @google/design.md lint` validates a `DESIGN.md` for the consistency of its token references, for
WCAG contrast ratios, and for conformance to the format's structural conventions, and returns its
result as JSON — which is what lets it run in CI and report per pull request. A companion `diff`
command compares two `DESIGN.md` files and returns the token-level changes between them in
structured form, putting design-system version control on a mechanical footing.

[[BlogPosting/division-of-labor-in-ai-instruction-files]] places the format as one of three layers of
instruction file handed to an AI agent, the layer covering appearance, alongside
[[DefinedTerm/agents-md]] for an agent's premises and `SKILL.md` for individual tasks. It is also the
layer that post treats as most explicitly split between machine-readable and human-readable content,
since the front matter and the body carry each separately rather than mixing them. In that post's
framing, the format's role is to gather a design system that had been spread across Figma files and
style-guide PDFs into one file that is readable both ways.

That post also records a gap for Japanese-language interfaces: the typography requirements specific
to Japanese — CJK font fallback, line height, letter-spacing, line-breaking rules and mixed-script
setting — are not defined in Google Labs' own samples, and a separate community repository
(`kzhrknt/awesome-design-md-jp`) publishes `DESIGN.md` files covering them for a number of Japanese
services. The suggestion made there is to use the two together rather than either alone.

Tooling has begun to treat the format as one output among several: the post names a CLI able to
generate and update a specification in either `SKILL.md` or `DESIGN.md` form, which it reads as a
sign of a toolchain built on the assumption that the layers are distinct.

## Related Terms

[[DefinedTerm/agents-md]], [[DefinedTerm/agent-skills]], [[DefinedTerm/ai-ide-rules]],
[[DefinedTerm/spec-driven-development]]
