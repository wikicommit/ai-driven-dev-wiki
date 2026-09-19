---
title: "GitHub Spec Kit"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, spec-driven-development]
sources:
  - type: url
    url: https://arxiv.org/pdf/2602.00180
    hash: sha256:982804fd917021d4811f4b23fc3ada9dfc07e4c91add2e07b32b2ffa9aad4253
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
  - type: url
    url: 'https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/'
    hash: sha256:c69d76f7139da5ec34ed3ad1c5ad12521c158fa6e73d753fdcf990baaa6cba75
  - type: url
    url: 'https://github.com/github/spec-kit'
    hash: sha256:43e53abd453112137f25876eef80951cf1caabd0b9b88260dc5c527de383c731
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An open-source toolkit that gives AI coding agents structured processes, reusable templates and documented outcomes. Its core process is spec-driven development, run as a sequence of human-gated agent skills; bug fixing and idea assessment ship as separate opt-in extensions."
  applicationCategory: "Spec-driven AI development toolkit"
  featureList: "specify CLI installed with uv; /speckit-* agent skills invoked in the agent's chat; spec-driven development, bug fixing and idea assessment as independent entry points; extensions, presets, workflows and bundles for customization; integrations across multiple coding agents"
  author: "[[Organization/github]]"
---

GitHub Spec Kit is an open-source toolkit for [[DefinedTerm/spec-driven-development]]. GitHub's 2025
announcement of it structures the workflow around AI coding assistants into four explicit, gated
phases, described first below; the repository now organises a larger command set and two further
processes around those phases, described under "Current Shape of the Toolkit". `/specify` generates a
detailed specification from a prompt, `/plan` creates the technical architecture, `/tasks` breaks
the plan into implementation tasks, and a final implementation step generates code task by task. At
each phase, a human reviews and refines the output before the workflow proceeds to the next one,
which is intended to keep the agent's output aligned with intent throughout the process rather than
only checked at the end.

## Capabilities

GitHub's own announcement of the toolkit (see
[[BlogPosting/spec-driven-development-with-ai-open-source-toolkit]]) sets out what each phase is
for. **Specify** takes a high-level description of what is being built and why, and has the agent
generate a detailed specification about user journeys, experiences and what success looks like
rather than technical stacks. **Plan** is where the developer supplies stack, architecture and
constraints — standardized technologies, legacy integrations, compliance requirements, performance
targets — and the agent produces a technical plan; GitHub notes multiple plan variations can be
requested for comparison, and that internal documentation made available to the agent can be folded
into the plan. **Tasks** breaks spec and plan into small reviewable chunks, each implementable and
testable in isolation, which GitHub likens to giving the agent a test-driven way to validate its own
work. **Implement** works through those tasks while the developer reviews focused changes rather
than large code dumps.

GitHub is explicit that the developer's role is not only to steer but to verify, and that the
checkpoints exist so gaps and omissions are caught before the next phase begins. In its own
description, the toolkit is installed by first installing the `specify` command-line tool, which
initializes the project structure, after which the workflow is driven by `/specify`, `/plan` and
`/tasks` commands. GitHub names GitHub Copilot, [[SoftwareApplication/claude-code]] and Gemini CLI
as coding agents it works with.

[[ScholarlyArticle/from-prompt-to-process]] describes the repository as organising commands such as
constitution, specification, plan, tasks and implementation, plus optional clarification, analysis and
checklist commands. It reports the toolkit's central idea, per Spec Kit's own documentation, as:
describe what to build, refine through structured phases, and let code agents implement from those
artifacts — with the specification acting as a source of truth rather than a disposable document.

## Adoption & Ecosystem

GitHub open sourced the toolkit, saying the approach is bigger than any one tool or company and
that the real innovation is the process rather than the tool; it describes Spec Kit as its
experiment in moving from "code is the source of truth" to "intent is the source of truth". The
three scenarios GitHub names as especially suited to it are greenfield projects, feature work in
existing systems — which it calls the most powerful case, because a spec forces clarity on how a
feature interacts with what already exists — and legacy modernization, where the original intent
has been lost and can be recaptured as a modern spec before rebuilding.

A 2026 practitioner's survey of spec-driven development tools ([[ScholarlyArticle/from-code-to-contract]])
categorizes GitHub Spec Kit, alongside [[SoftwareApplication/kiro]] and [[SoftwareApplication/tessl]],
as one of three representative AI-assisted SDD toolkits that structure coding workflows explicitly
around specifications.

Under the [[DefinedTerm/six-dimension-process-taxonomy]], Spec Kit scores 2 on specification, 1 on
context, 1 on roles, 1 on execution, 1 on validation and 2 on portability — a total of 8 out of 12.
That study reads the profile as high portability bought at the cost of roles and validation: it puts
Spec Kit alongside [[SoftwareApplication/openspec]] as one of two SDD toolkits competing on the same
ground, with Spec Kit the more complete in phases and portability and OpenSpec the lighter. The scores
express that study author's judgement from official documentation rather than an independent empirical
measurement, and the study records that Spec Kit had not been through independent academic evaluation.

The fragility that study names is dependence on interpretation: a clear specification helps, but does
not guarantee that implementation, tests and maintenance stay aligned without additional checks, and
the dominant risk it records for Spec Kit is drift between the artifacts and the implementation where
validation is weak.

## Current Shape of the Toolkit

The project's own repository presents a wider toolkit than the four-phase account above. Spec Kit describes itself as giving AI coding agents structured processes, reusable
templates and documented outcomes, and offers three processes as **independent entry points rather
than three mandatory phases**: spec-driven development for building a feature or application, bug
fixing for diagnosing and repairing broken behaviour, and idea assessment for deciding whether an
idea deserves investment. Spec-driven development ships in core; the other two are opt-in bundled
extensions installed with `specify extension add bug` and `specify extension add assess`.

Setup is a CLI install (`uv tool install specify-cli`) followed by
`specify init <project> --integration <key>`, where the integration key selects which coding agent
the project is wired for; the documented prerequisites are Python 3.11+, `uv`, and a supported
agent on Linux, macOS or Windows. The processes themselves are then driven from inside the agent's
chat as `/speckit-*` **agent skills, not terminal commands** — the repository is explicit on that
distinction, and on invoking them one at a time and reviewing each result before continuing.

The spec-driven sequence the repository documents runs `/speckit-specify`, `/speckit-plan`,
`/speckit-tasks`, `/speckit-implement` and `/speckit-converge`, with **implement and converge
repeated until convergence reports "Converged"** — a loop the earlier four-phase framing has no
counterpart for. Clarification, checklist and consistency-analysis commands are available as
additional quality gates. The bug-fixing process (`/speckit-bug-assess`, `/speckit-bug-fix`,
`/speckit-bug-test`) keeps diagnosis, repair and verification separate so that the fix addresses the
assessed cause and the check tests the original symptom; its reports land under `.specify/bugs/<slug>/`
and end in a verdict of `verified`, `partial` or `failed`, with the repository stating that missing
verification is not a successful fix. The assessment process
(`/speckit-assess-intake`, `-research`, `-define`, `-shape`, `-decide`) works even in a project with
no source code and ends in a `go`, `needs-clarification` or `kill` decision; the repository notes
that stopping with a documented reason is also a useful result, and that a `go` decision can be
handed to `/speckit-specify` if the idea is to be built.

Customization is layered: extensions add capabilities, presets adapt existing behaviour, workflows
automate steps, and bundles package a role-based setup, with project-local overrides for one-off
template changes. The toolkit is MIT licensed.
