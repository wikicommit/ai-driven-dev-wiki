---
title: "Continuous AI"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-engineering, ci-cd, engineering-practice]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/generative-ai/continuous-ai-in-practice-what-developers-can-automate-today-with-agentic-ci/'
    hash: sha256:994d27bdd399c24187602b4764046df3b5e7b67fb9de1d565cff3b8821304ac3
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A pattern proposed by GitHub Next in which background agents run inside a repository the way CI jobs do, but for work that requires judgment rather than deterministic rules. Summarized as natural-language rules plus agentic reasoning, executed continuously, producing reviewable artifacts rather than autonomous commits."
---

Continuous AI is a pattern in which background agents operate inside a repository the way continuous
integration jobs do, but are reserved for tasks that require reasoning instead of rules. GitHub
frames it in [[BlogPosting/continuous-ai-in-practice]] with a one-line formulation: natural-language
rules plus agentic reasoning, executed continuously inside your repository. In practice that means
expressing in plain language what should be true about a codebase — particularly where that
expectation cannot be reduced to rules or heuristics — and having an agent evaluate the repository
and produce artifacts a developer can review, such as suggested patches, issues, discussions or
insights.

The pattern is defined against CI rather than as a replacement for it. CI is characterized as
designed for binary outcomes and as excelling where correctness can be expressed unambiguously,
which the source treats as a strength rather than a shortcoming; Continuous AI is positioned as a
different class of automation for the cases where correctness depends on interpretation and intent.
The post is explicit that it is not a new product, that traditional CI remains essential, and that
where a problem can be expressed deterministically, extending CI is the right approach.

## Usage

The work it is aimed at is characterized as judgment-heavy and context-dependent — whether intent
still holds. The illustrations given are a docstring that disagrees with its implementation, text
that passes accessibility linting yet still confuses users, a dependency that changes behavior
without a major version bump, a regex compiled inside a loop, and UI behavior visible only through
interaction.

Workflows are written as statements of intent with constraints and permitted outputs, the source's
examples including checking whether documented behavior matches implementation and proposing a
concrete fix, generating a weekly report on activity and bug trends, flagging performance
regressions in critical paths, and detecting semantic regressions in user flows. The source cautions
against reading these as one-liners: developers are said to rarely author such workflows in a single
pass, instead collaborating with an agent to refine intent and define acceptable outputs.

Seven categories are presented as tested in real repositories rather than theoretical:
reconciling documentation with behavior; producing recurring reports that synthesize across issues,
pull requests, commits and CI results, where the stated value is the synthesis rather than the
report; regenerating translations when source text changes; detecting dependency drift, including a
reported demo in which an agent diffed CLI help text against previous days and filed an issue about
an undocumented flag; burning down test coverage; making background performance improvements; and
automated interaction testing, using agents as play-testers to detect UX regressions.

## When It Applies

The pattern applies where an expectation about a codebase matters but cannot be reduced to a rule
without losing meaning — the test offered by the head of GitHub Next being whether the task can be expressed as a rule or a flow chart.
It assumes a repository with an event system to trigger on, and an agent permitted to act only
within declared bounds.

Its stated safety precondition is [[DefinedTerm/safe-outputs]]: agents operate read-only by default,
and may produce only the artifacts a workflow explicitly permits. The division of labour it assumes
is that developer judgment remains the final authority — agents do not merge code, and the source
describes the pattern as helping scale that judgment across a codebase rather than replacing it. It
is misapplied to deterministic work, where the source itself says YAML, schemas and heuristics
remain the correct tools.

How well-established it is: this is one vendor's research pattern, explored by its R&D group and
exercised through a prototype that compiles a workflow into a CI action. The categories above are
reported as tested in real repositories. Most are described without effectiveness measurements; the
test-coverage case is the exception, reported as taking coverage from about 5% to near 100% with
more than 1,400 tests across 45 days for about $80 worth of tokens.

## Related Terms

- [[DefinedTerm/safe-outputs]] — the permission model the pattern depends on
- [[BlogPosting/continuous-ai-in-practice]] — the source of this account
- [[DefinedTerm/agentic-coding]] — the broader practice this applies to repository automation
- [[DefinedTerm/human-in-the-loop]] — the review checkpoint the pattern preserves
- [[DefinedTerm/code-review-as-runtime-monitoring]] — a related use of review as a continuous control
