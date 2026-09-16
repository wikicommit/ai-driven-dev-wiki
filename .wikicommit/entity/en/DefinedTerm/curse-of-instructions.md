---
title: "Curse of Instructions"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/good-spec/'
    hash: sha256:fbb1e0c078b1d920689cbc3c652ad4bf253d5b39c77f957cab7ee4e6cd1ff5fa
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A finding that a language model's adherence to individual instructions drops significantly as more directives are piled into a single prompt, so that presenting many rules at once means some are followed and others are overlooked."
---

The curse of instructions is a named research finding that a language model's ability to follow each individual instruction drops as more instructions are combined into a single prompt. Research on the effect reportedly found that even GPT-4 and Claude struggle to satisfy many requirements simultaneously: presented with ten detailed rules, a model may follow the first few and start overlooking the rest.

## Usage

The finding is cited as the reason to decompose a large specification into sequential, simple instructions rather than a single prompt listing everything at once — focusing a model on one sub-problem at a time, completing it, and then moving to the next, rather than presenting the full requirement set together.

## Related Terms

[[BlogPosting/good-spec]]
