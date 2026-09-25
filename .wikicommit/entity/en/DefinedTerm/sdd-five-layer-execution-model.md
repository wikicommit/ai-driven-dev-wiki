---
title: "SDD five-layer execution model"
type: "schema:DefinedTerm"
lang: en
tags: [spec-driven-development]
aliases: ["Five-layer execution model"]
sources:
  - type: url
    url: 'https://www.cnblogs.com/studyzy/p/19638317'
    hash: sha256:105218db5ca2d8c9d618572ca661b03b7775fd1a43df1b7ac3e8137ff20f5f78
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A layered model of spec-driven development, set out in a February 2026 Chinese-language blog post, that chains intent, implementation, verification and governance through five top-down layers: specification, generation, execution, validation and governance."
---

The SDD five-layer execution model is a way of structuring
[[DefinedTerm/spec-driven-development]] (SDD) described in a Chinese-language post on the 深蓝居 blog
(February 2026). The post presents it as the "skeleton" of SDD: a top-down chain in which each layer
constrains the one below it, with defined inputs, outputs and responsibilities, so that the
specification's authority runs through the whole system from intent to implementation, verification
and governance. The five layers, from the bottom up, are the **specification layer** (declarative
intent — API models, message contracts, domain patterns, policy constraints), the **generation layer**
(turning intent into executable form, such as cross-language code, type definitions and SDKs), the
**execution layer** (the runtime implementation, with a human-governed skeleton architecture and
AI-generated business logic), the **validation layer** (contract tests, schema validation and
interception of drift from the specification) and the **governance layer** (version management,
security policy and human-in-the-loop decisions about how the specification evolves).

## Usage

The post walks a user-registration interface through the layers: the specification layer defines the
request and response formats, error codes and security requirements; the generation layer produces the
corresponding Go structs, API documentation and client SDK; in the execution layer AI writes the
business logic while humans own the core architecture; the validation layer continuously compares the
code with the specification and raises an alert on any deviation; and the governance layer handles
specification version upgrades, permission control and human review of key changes. As an example of
the generation layer, it shows an OpenAPI schema converted into Go types by a code generator such as
oapi-codegen.

The model rests on what the post calls architectural determinism — the idea that the specification,
not the code, is the highest authority and that the implementation must continuously align with it.
Drift detection is the technique it names for this, turning architecture from a design-time document
into a runtime constraint.

## Related Terms

- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/spec-driven-development-levels]]
- [[DefinedTerm/human-in-the-loop]]
