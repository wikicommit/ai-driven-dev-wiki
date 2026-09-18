---
title: "Data-Aware Testing"
type: "schema:DefinedTerm"
lang: en
tags: [agents, tool-use]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2504.15546'
    hash: sha256:39549788a2452ec0fb8ea5da808b3e0e1e78cd4676d00b50ff2c06f8b85de2cd
review_status: pending
generated_at: "2026-09-17"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A test-generation technique, proposed by Bandlamudi et al. in their REST-API-as-LLM-tool testing framework, that augments LLM-generated test cases with real inter-tool data dependencies — captured in a tool dependency graph — so generated inputs reflect values a tool would actually receive at run time, rather than syntactically valid but semantically irrelevant values the LLM invents on its own."
---

Data-aware testing is a test-case generation technique, proposed in [[ScholarlyArticle/testing-rest-apis-as-llm-tools]], that grounds an LLM's generated test inputs in enterprise-specific data obtained from other tools in the same catalog, rather than letting the LLM invent input values on its own. Purely LLM-generated test cases can be syntactically valid while containing irrelevant data — for example a fabricated user ID — which the paper reports produces empty responses, trivial outputs, or "no results found" errors (e.g. a 404 response), especially for tools whose valid inputs (a real record ID, an existing account number) are available only at run time and cannot be inferred from the API specification alone.

## Usage

To generate a data-aware test input for a target tool, the framework first builds a tool dependency graph: an LLM inspects the tool catalog's docstrings to infer, for each pair of tools, whether one tool's output parameters can supply another tool's input parameters, and — once a human tool builder has verified the inferred parameter mappings — the graph is persisted with tools as nodes and the identified dependencies as edges. To test one target tool, the framework identifies the ordered chain of tools that feeds it, executes that chain, and maps each parent tool's transformed outputs into the next tool's inputs until it reaches values that satisfy the target tool's own specification; those values become the data-aware test input. In an evaluation on 705 test cases with an approved dependency graph, using data-aware inputs instead of LLM-invented ones reduced empty-output and output-mismatch error rates by around 10 percentage points each and increased the fraction of test cases executing without any error, compared with the same test cases generated without data-aware inputs.

## When It Applies

Data-aware testing applies specifically to enterprise tool catalogs where tools have real inter-tool data dependencies — a value one tool's response supplies as another tool's input — that an API specification alone does not expose. It assumes a tool dependency graph has already been built and reviewed by a human tool builder before use. The paper notes that dependency and parameter-mapping inference can be unreliable when a tool's own docstring lacks detailed parameter descriptions, since the LLM used to infer dependencies relies on those docstrings.
