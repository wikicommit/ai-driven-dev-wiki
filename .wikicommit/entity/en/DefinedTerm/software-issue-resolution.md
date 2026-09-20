---
title: "Software Issue Resolution"
type: "schema:DefinedTerm"
lang: en
tags: [agents, software-maintenance]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.22256'
    hash: sha256:9a5a75e55b1a5f5818704198234c0c775aeeaaf8ae884348416af572766c9cd2
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The task of understanding, locating and resolving issues in a real code repository from a developer's natural-language description of the problem, producing a repository-level patch. It spans diverse maintenance activities — bug fixes, feature additions, efficiency optimisation — and does not assume a test exists that triggers the reported behaviour."
---

**Software issue resolution** is the task of understanding, locating and resolving issues in
real-world code repositories on the basis of developers' natural-language descriptions of them. In
its automated, end-to-end form it takes an issue description and a code repository as input and
produces a repository-level patch that resolves the issue. It covers diverse maintenance activities,
including bug fixes, feature additions and efficiency optimisations, and it is a part of software
maintenance, which
[[ScholarlyArticle/agentic-software-issue-resolution-with-large-language-models]] reports as
accounting for about two-thirds of software lifecycle costs.

## Usage

The term is used to mark out a task boundary. That survey argues that issue resolution should not be
treated as a sub-case of automated program repair, on two grounds: it encompasses more diverse
maintenance activities than repair does, and — even for bug-fixing issues — it does not assume the
existence of tests that can trigger the bug. The second point has consequences for how a system is
built, since generating a test that reproduces the reported behaviour becomes part of the work rather
than a given.

The same survey abstracts the automated task into five logical phases, which it stresses denote
functions rather than a fixed execution order, so a system may run them sequentially or interleave
them dynamically at inference time:

- **Repo preprocessing** — constructing an accessible, comprehensible knowledge representation of the
  repository, such as a tree of files, classes and functions or a graph that additionally encodes
  calls, inheritance, imports and references.
- **Localization** — identifying the code snippets most likely responsible for the reported issue,
  narrowing the search space for the phases that follow.
- **Repair** — generating candidate patches for the located code, typically several, to maximise the
  chance of producing a correct fix.
- **Patch validation** — generating reproduction tests that simulate the issue scenario, or selecting
  regression tests that check the candidate patch has not broken existing behaviour, and filtering
  out patches that fail.
- **Patch selection** — choosing the most promising candidate for submission, by self-consistency
  voting over normalised patches or by having a model assess each candidate against the issue.

The survey is explicit that the phases are diagnostic rather than sufficient: dedicated localization
methods have been shown to raise end-to-end resolution rates when fed into downstream patch
generation, and generated reproduction tests are widely used to filter and rerank candidates, but
correct localization does not guarantee a correct patch and weak reproduction tests may accept
patches that are plausible yet behaviourally incorrect.

## Related Terms

- [[DefinedTerm/ai-coding-agent]] — the kind of system the task is now predominantly attempted with
- [[DefinedTerm/repository-level-coding]] — the broader setting the task operates in
- [[Dataset/swe-bench]] — the benchmark whose introducing paper the survey credits with pioneering the task
