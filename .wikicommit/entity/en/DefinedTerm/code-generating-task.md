---
title: "Code-Generating Task"
type: "schema:DefinedTerm"
lang: en
tags: [code-generation, software-engineering, taxonomy, program-repair]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.25536'
    hash: sha256:84c75544b09d7855a70f7e1f4cfdd0942a5ef7c015bc8053143fd65c3c23992d
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An umbrella term for a software engineering task whose primary output is an automatically generated code artefact intended to be compiled or interpreted and executed, proposed to scope study of LLM-based code generation."
---

A code-generating task (CGT) is a software engineering task whose primary output is an automatically generated code artefact, written in a programming language and intended to be compiled or interpreted and executed. The definition is proposed in [[ScholarlyArticle/tertiary-review-of-llm-based-code-generating-tasks]] as a unifying umbrella, on the grounds that existing research treats code-producing tasks either in isolation or within the much broader context of software engineering as a whole, leaving the field without a shared scoping for them.

Two boundaries come with the definition. Tests written as code and repair patches count as CGT output, since both are executable artefacts. Tasks that produce only non-executable text — inline code comments, docstrings, documentation — are explicitly not CGTs. The scale of output is left open: a CGT may operate at the level of a line or token, as in code completion, or at the level of a package or whole system, as in program synthesis. Inputs vary similarly, and may include natural language, existing code, documentation, images and other forms.

## Usage

The term exists to make a body of evidence comparable. The review that proposes it argues that prior secondary studies are either too broad — covering the whole intersection of machine learning and software engineering — or too narrow, confined to a single task such as software testing, which makes it difficult to isolate the state of evidence specifically for LLM-based code generation. Separately, in positioning its own scope against earlier tertiary reviews, the review describes its set of CGTs as somewhat orthogonal to a SWEBOK knowledge area.

The review compiles a working set of named CGTs, each characterised by its input-to-output shape: code generation (natural language, examples or formal specifications to code); program synthesis (the same, at larger scale); code completion (code context to the next lines or blocks, conditioned on local context); patch generation as part of program or vulnerability repair (code to repaired code); test generation (specifications or code to tests as code); code translation (code to code, migrating across languages while preserving functionality); and refactoring (code to functionality-preserving code).

Consolidating the heterogeneous labels used across the 30 secondary studies onto these categories changes which task looks dominant. Patch generation and repair becomes the most frequently reported CGT at 22 studies, once terms such as program repair, vulnerability repair, bug repair and bug fixing are aggregated — ahead of code generation at 20, code translation at 9 and code completion at 8. Program synthesis, test generation and refactoring appear less frequently. A handful of labels reported in the literature, including code co-evolution, code editing, method name generation and testing repair, could not be mapped directly onto the definitions, though the authors describe them as closely related to refactoring or repair activities.

## Related Terms

- [[DefinedTerm/agentic-coding]]
- [[DefinedTerm/code-review-agent]]
