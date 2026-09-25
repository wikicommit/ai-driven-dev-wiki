---
title: "Repository-level coding"
type: "schema:DefinedTerm"
lang: en
tags: [terminology, software-engineering, agents, llm]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2309.12499'
    hash: sha256:19aa6b297c4058cd751158ab0079977a52e09e89b57a947614dda5da3fa328da
  - type: url
    url: 'https://arxiv.org/html/2406.01422v2'
    hash: sha256:d9bfa615cea940d9674ffc433e47eb528cb25093699809cd3e9b54dabf0caf1d
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A formulation, introduced by the CodePlan paper, of software engineering activities that involve pervasively editing an entire code repository rather than a single localized site — package migration, fixing static-analysis or test error reports, and adding type annotations or other specifications."
---

Repository-level coding is the term
[[ScholarlyArticle/codeplan-repository-level-coding-using-llms-and-planning]] uses for software
engineering activities that involve pervasively editing the entire repository of code, as opposed to
solving a problem at one localized site. The activities that paper groups under the formulation are
package migration, fixing error reports coming from static analysis or testing, and adding type
annotations or other specifications to a codebase.

## Usage

The formulation is introduced to mark a boundary in what large language models can be asked to do
directly. The same paper observes that LLM-powered tools such as GitHub Copilot have succeeded in
offering high-quality solutions to localized coding problems, and argues that repository-level tasks
are more involved and cannot be solved directly using LLMs. Two properties are given as the reason:
code within a repository is inter-dependent, so an edit in one place has consequences elsewhere, and
the entire repository may be too large to fit into the prompt.

Because of those two properties, the term marks tasks whose difficulty is structural rather than a
matter of the individual edit being hard. In the evaluation reported alongside the formulation, the
repository-level tasks studied — package migration in C# and temporal code edits in Python —
required inter-dependent changes to between 2 and 97 files per repository.

The same two obstacles reappear, stated independently, in work on issue resolution.
[[ScholarlyArticle/lingmaagent-improving-automated-issue-resolution]] does not use this term, but
argues from the same starting point: a repository may contain thousands of files, too many to place in
a model's context — and a model given an extensive context would still struggle to find the relevant
code — while the code for one functionality is logically scattered across folders and files rather
than laid out in sequence, so that the place where a bug raises an error and the place that needs
changing may sit in different files. Its response is to condense the repository into a knowledge
graph of files, classes, functions and call relationships and to search that graph, rather than to
plan a chain of edits.

## Related Terms

- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/agentic-coding]]
- [[DefinedTerm/software-issue-resolution]]
