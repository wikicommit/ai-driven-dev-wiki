---
title: "Cursor"
type: "schema:SoftwareApplication"
lang: en
tags: [ai-assisted-programming, coding-tools]
sources:
  - type: url
    url: https://simonwillison.net/2025/Mar/19/vibe-coding/
    hash: sha256:653ba52b66ad62da601ae6fd257897841726d7ac6a07029edc6d0e1c5b12188f
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "A popular tool for building software with an LLM, initially intended for professional developers and carrying far fewer safety rails than sandboxed alternatives."
---

Cursor appears in [[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]] as a popular tool
used for [[DefinedTerm/vibe-coding]] that was not originally designed for it. Simon Willison notes
that it was initially intended for professional developers, and treats that origin as the
explanation for how little it constrains what generated code can do.

## Capabilities
The post's one direct characterisation is comparative: Cursor has far less in the way of safety
rails than [[SoftwareApplication/claude-artifacts]], whose sandbox prevents unreviewed code from
reaching the network or from causing harm outside the project.

Karpathy's account of vibe coding, quoted in the same post, names Cursor Composer driven by a
Sonnet model as the setup he was working in, and describes talking to it by voice rather than
typing. That is his description of his own workflow at the time rather than a statement about what
the product generally offers.

## Adoption & Ecosystem
Willison groups Cursor with other popular vibe coding tools, which places a tool built for
professionals among the ones newcomers reach for. The safety concern he raises follows from exactly
that mismatch: the conditions he sets out for vibe coding — low stakes, care with secrets and
private data, hard billing limits — have to be met by the person rather than by the tool when the
tool does not enforce them.
