---
title: "DeepCode"
type: "schema:SoftwareApplication"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.07921'
    hash: sha256:314c8fd358fe756fabd1a16577a270aadea8b7375da1f84868c4809b3eb32278
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "An open-source agentic coding framework, published by researchers at The University of Hong Kong, that synthesizes a complete code repository from a document such as a scientific paper by orchestrating blueprint distillation, stateful code memory, retrieval-augmented knowledge injection, and closed-loop sandbox verification."
  applicationCategory: "Agentic coding framework"
  author: "The University of Hong Kong"
---

DeepCode is an open-source agentic coding framework, published by researchers at The University of Hong Kong, for synthesizing a complete, executable code repository from a document — most centrally, reproducing a scientific paper's experiments as code using the paper as the sole specification. Its source code is published on GitHub at HKUDS/DeepCode.

## Capabilities

The framework accepts a target document in PDF or Markdown form and produces a repository through three phases: a Blueprint Generation phase that distills the document into a structured implementation blueprint (project file hierarchy, per-module component specifications, a verification protocol, and an execution-environment specification); a Code Generation phase that synthesizes files iteratively against that blueprint using a stateful memory of already-generated files (CodeMem) and a retrieval-augmented system (CodeRAG) that pulls in patterns from external repositories only when needed; and an Automated Verification phase that runs static analysis followed by sandboxed execution, feeding runtime errors back into an iterative repair loop.

On the PaperBench Code-Dev benchmark (20 ICML papers, graded by an automated judge), it is reported to score 73.5±2.8 on average, versus 43.3±1.1 for the best general-purpose LLM-agent baseline and 51.1±1.4 for a specialized scientific-code-agent baseline (PaperCoder); on a 5-paper subset run with the same underlying model (Claude Sonnet 4.5-thinking), it scored 0.8541 versus 0.5871 for Claude Code, 0.5841 for Cursor, and 0.3997 for Codex.

## Adoption & Ecosystem

The framework is evaluated specifically for scientific-paper reproduction and general document-to-software synthesis, and is compared in its publication against both general-purpose commercial coding agents (Cursor, Claude Code, Codex) and specialized scientific-code-reproduction tools (PaperCoder).
