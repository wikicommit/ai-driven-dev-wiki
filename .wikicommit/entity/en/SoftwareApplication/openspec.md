---
title: "OpenSpec"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, spec-driven-development]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
  - type: url
    url: 'https://timdeschryver.dev/blog/keep-agentic-ai-simple-a-practical-workflow-for-software-development'
    hash: sha256:4f5e3967c2bcf26ffa62d57bb3d9eac62c5b65949a33d44e26d4ae20bfcb810c
  - type: url
    url: 'https://github.com/ForceInjection/OpenSpec-practise'
    hash: sha256:e21ef4609f01b99fcb3b246c274f32aef2f20956b316b9b16f2272bbbb3bcc6a
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5"
generated_with: "0.9.0"

properties:
  description: "A lightweight specification-driven development framework that concentrates intent into a single unified specification and traceable change proposals, aiming for low process overhead and broad compatibility across code assistants."
  applicationCategory: "Spec-driven AI development framework"
  featureList: "Unified single specification; structured change-management flow; slash-command integration across many code assistants; explore-first workflow; diff-only review of spec deltas; validation findings report"
---

OpenSpec is a framework for [[DefinedTerm/spec-driven-development]] that positions itself on
simplicity and low process overhead. Its stated goal is aligning human and AI on requirements before
coding begins, and its official repository describes support for dozens of code assistants through
slash commands together with a structured change-management flow. It is one of the six frameworks
assessed in [[ScholarlyArticle/from-prompt-to-process]].

## Capabilities

Where heavier frameworks accumulate artifacts and phases, OpenSpec's declared differentiator is
reducing process friction: it concentrates the intention into a single specification and into
traceable change proposals rather than a progression of separate documents. That study places it
alongside [[SoftwareApplication/github-spec-kit]] as one of two SDD toolkits competing on the same
ground, with OpenSpec the lighter of the two and Spec Kit the more complete in phases and portability.

A practitioner account, [[BlogPosting/keep-agentic-ai-simple]], shows what that looks like in use.
From a few sentences of prompt describing a feature, OpenSpec generated three files for its author:
a `proposal.md` with the functional analysis (a summary, what and why, what is in and out of scope,
and success criteria), a `design.md` with the technical design, and a `tasks.md` with an ordered,
step-by-step implementation plan. He could revise them with further prompts or by editing them by
hand, found the default templates good enough, and notes that the archived documents are committed
with the rest of the code.

A community practice repository, [OpenSpec Practise](https://github.com/ForceInjection/OpenSpec-practise),
documents the workflow in more detail as of OpenSpec v1.13.0. There, `openspec init --tools claude`
generates slash commands and matching skill files in a `.claude/` directory:
`/opsx:explore`, `/opsx:propose`, `/opsx:update`, `/opsx:apply`, `/opsx:sync` and `/opsx:archive`. Explore
acts as a thinking partner that investigates the codebase, weighs options and clarifies requirements before
any spec or code is written; propose starts a change, with `openspec instructions` supplying templates and
context; update revises the planning documents during implementation; apply has the AI implement the code
from the spec; sync merges the change's delta specs into the main specification before archiving; and
`openspec archive` moves the change into an archive directory. The repository stresses that the stages are
not locked: the spec can be revised at any point and exploration can happen at any stage. Its worked
examples are labelled by release: one walks through explore, propose, apply, sync and archive under
v1.5.0, one demonstrates update under v1.7.0, and one shows archive's built-in spec merge under v1.11.0.

In that repository's layout, an `openspec/config.yaml` holds project context such as the tech stack and
conventions and is injected into every AI planning request; `openspec/specs/` holds the main specification
per capability; and each change carries a `proposal.md` (why, what changes, capabilities), a `design.md`,
a `tasks.md` and delta specs for the capabilities it touches, with scenarios written in Given/When/Then
form. For review, `openspec show <change> --diff` renders only the lines that actually changed, although a
MODIFIED requirement must restate all of its retained scenarios (shown in its v1.11.0 example); `openspec
validate --report findings` produces a focused report of warnings and errors (its v1.13.0 example), which
the repository reports found
three real spec problems on its first run against one of its examples. A beta feature called stores lets
planning live in a separate repository that several code repositories reference as read-only context.

## Adoption & Ecosystem

Under the [[DefinedTerm/six-dimension-process-taxonomy]], OpenSpec scores strongly on specification
and portability and weakly elsewhere: its assessed profile is 2 for specification, 1 for context, 0
for roles, 1 for execution, 0 for validation and 2 for portability. The portability score reflects
compatibility with many assistants, which the paper reads as positioning the framework as a thin layer
over the agent. The assessment is the study author's own judgement from official documentation, not an
independent empirical measurement, and the framework had not been through independent academic
evaluation at the time of writing.

The trade-off the study names is coverage: the low overhead that makes OpenSpec attractive for
pointwise changes may fall short when a project requires more elaborate roles, architecture and
validation. The study reports the same pattern — high portability bought at the cost of roles and
validation — for both OpenSpec and Spec Kit, though its table has OpenSpec at 0 on each of those two
dimensions where Spec Kit is at 1. That pairing is what the study reads as the most informative pattern
in its results: an opposition between process depth and portability.

That practitioner used OpenSpec only for larger features — starting from its propose skill to produce
a plan, then having the coding agent implement it — and prompted the agent directly for small changes
and bug fixes. In his experience, larger features built without a spec often missed subtle details
and took more iterations, which is one person's account rather than a measured comparison.

The OpenSpec Practise repository uses one set of OpenSpec specifications to drive two implementations of a
minimal e-commerce system, a zero-dependency Node.js version and a Python version built on FastAPI and
Pydantic. It also proposes a mapping from [[DefinedTerm/domain-driven-design]] onto OpenSpec's structure,
drawn from a companion DDD skills project: a bounded context becomes a domain directory under `specs/`, a
domain service or command becomes a requirement, aggregate behaviour becomes a scenario, an application
service becomes the technical design, and the tactical design backlog of entities, value objects and
repository interfaces becomes the task list.

Note that one of the public tool comparisons the study consulted during its directed search was
published from the OpenSpec portal, and the paper cites it alongside OpenSpec's own material in its
characterization of the framework; the paper flags it as a case of product content written by one of the
tools being compared.
