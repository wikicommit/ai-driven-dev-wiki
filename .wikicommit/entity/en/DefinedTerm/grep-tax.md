---
title: "grep tax"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, tokens, terminology]
sources:
  - type: url
    url: 'https://simonwillison.net/2026/Feb/9/structured-context-engineering-for-file-native-agentic-systems/'
    hash: sha256:3f82de188c24399ccbce66e5e53af94f0076aa296322a4b9d6a662e0554d1406
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The token overhead a model incurs when a context format is compact on disk but unfamiliar to the model, so that it burns more tokens across repeated refinement attempts than a larger, familiar format would have cost."
  termCode: ""
  inDefinedTermSet: ""
---

The "grep tax" is the name given to a result in which a deliberately token-efficient data format ends up costing *more* tokens in practice, because the model's unfamiliarity with the syntax stops it from constructing effective refinement patterns and it iterates repeatedly instead. It is reported in a paper that [[Person/simon-willison]]'s link blog summarises and quotes, and the term comes from that paper's own figure caption.

## Usage

The finding concerns TOON — Token-Oriented Object Notation — a format intended to represent structured data in as few tokens as possible. As relayed in that link post, TOON files were roughly 25% smaller than the equivalent YAML, yet consumed dramatically more tokens as schema size grew: 138% more than YAML at a 500-table schema, rising to 740% more at 10,000 tables. The stated root cause is that models lacked familiarity with TOON's syntax and so could not construct effective refinement patterns; those scale experiments used Claude models only.

Willison's own summary of why the detail matters is that it is a counterexample to the intuition that a smaller serialisation is a cheaper one: what a model can *work with* iteratively matters more than what it costs to state once.

The surrounding study, as the post quotes it, used SQL generation as a proxy for programmatic agent operations across 9,649 experiments, 11 models, 4 formats (YAML, Markdown, JSON, TOON) and schemas from 10 to 10,000 tables. Its largest effect, in Willison's reading, was the models themselves — with frontier models beating leading open-source models — and only the frontier models benefited convincingly from filesystem-based context retrieval, which he takes as reinforcing his sense that filesystem coding-agent loops are not yet handled as well by open-weight models.

## Related Terms

The grep tax is a specific failure of [[DefinedTerm/context-engineering]] at the encoding layer rather than the selection layer: the question is not which information reaches the model but in what notation. It sits alongside [[DefinedTerm/context-rot]] as a reason that raw token count is a poor proxy for how well a context actually works.
