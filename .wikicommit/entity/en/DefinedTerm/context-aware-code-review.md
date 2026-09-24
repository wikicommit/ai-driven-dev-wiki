---
title: "Context-aware code review"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, context-engineering]
sources:
  - type: url
    url: 'https://aise.phodal.com/aise-code-review.html'
    hash: sha256:c66c9a026df66e7f4feae11ee51fd39f0d6479793176e5269c0d01403e7f9453
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Code review that judges a change against the wider system it lands in — project conventions, existing code, infrastructure and performance, security, and consistency with existing interfaces — rather than the diff in isolation; a recurring design goal of AI code review tools."
---

Context-aware code review is reviewing a code change against the wider system it lands in rather than the diff alone: whether the change fits the existing system, what it affects in the software's infrastructure, and whether it follows best practice. Taking an API change as its example, Phodal's chapter on AI-assisted code review, drawing on a CodeRabbit article, describes such a review as checking the API's compatibility with existing systems and its impact on the software infrastructure, so that it integrates smoothly into the existing framework.

## Usage

The chapter lists the factors such a review commonly weighs:

- **Coding standards** — project-specific conventions such as file naming and directory structure, and whether the change reuses existing libraries, classes or methods instead of duplicating them.
- **Impact on existing code** — whether the change introduces bugs, what additional tests are needed, and whether API or user documentation needs updating.
- **Infrastructure and performance** — whether a database or API migration is needed, and whether performance elsewhere in the codebase could degrade.
- **Security and robustness** — trying to "break" the change to expose bugs or vulnerabilities.
- **Consistency and optimisation** — consistency of a new API with existing ones, whether the changelog entry is accurate, and whether the proposed solution is the best fit for the problem.

In its survey of AI code review tools, the chapter calls "context is king" a recurring theme and reads the tools' different approaches — retrieval-augmented generation, code graph analysis, whole-codebase analysis — as competing ways of supplying project-specific context, a direct response to what it identifies as the main limitation of early AI review tools, their lack of context awareness. It names [[SoftwareApplication/coderabbit]]'s code graph analysis and Sourcegraph Cody's retrieval over code search among the examples.

## When It Applies

The approach assumes the reviewer, human or AI, can see enough of the codebase to judge a change's fit, which for an AI reviewer means deciding how much surrounding code to supply. The chapter's account of [[SoftwareApplication/sourcery]] marks where this goes wrong: supplying more context gives diminishing returns and, past a point, reduces accuracy — producing false positives or hallucinated review comments — while also being expensive. Sourcery's response is to add context selectively, expanding only the diff chunks that survive a deterministic filter. In the chapter the practice is presented as a principle drawn from AI review tool vendors' own writing rather than as a measured result.

## Related Terms

- [[DefinedTerm/agentic-code-review]]
- [[DefinedTerm/code-review-agent]]
- [[DefinedTerm/context-engineering]]
