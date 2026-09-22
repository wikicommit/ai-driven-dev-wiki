---
title: "cc-sdd"
type: "schema:SoftwareApplication"
lang: en
tags: [spec-driven-development, coding-agents, agents, coding-tools, cli]
sources:
  - type: url
    url: 'https://sreake.com/blog/learn-about-spec-driven-development/'
    hash: sha256:e8daa5b4df3be65a4f9ac7fc508f2c5e3a691b64fb7a69809011b0c17c3dba37
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "An npm package that installs a spec-driven development workflow into an AI coding agent as a set of slash commands, keeping requirements, design and tasks as Markdown in the repository. Its design is inspired by Kiro's spec-driven development and is compatible with Kiro specifications."
  applicationCategory: "Spec-driven development toolkit"
  featureList: "Slash commands for steering, spec initialisation, EARS-format requirements, technical design, task breakdown and implementation; support for eight coding agents; specification output in thirteen languages; dry-run and backup installation flags"
---

cc-sdd is an npm package that brings [[DefinedTerm/spec-driven-development]] to an AI coding agent,
installed with a single `npx` invocation and then driven entirely through slash commands. Its stated
purpose is to keep requirements, design and tasks as Markdown files in the repository while
development proceeds in collaboration with the agent, so that the staged progression from
requirements to implementation — and the review point at each stage — is available without leaving
the agent's interface.

Its design is attributed to inspiration from [[SoftwareApplication/kiro]]'s spec-driven development,
and it is compatible with Kiro specifications, which
[[BlogPosting/introduction-to-cc-sdd]] — the introductory guide this page is written from — gives as
what makes best practices originating with Kiro directly reusable under it.

Installation writes into two places: slash commands go under the agent's own command directory, and
templates plus generation rule files go under a `.kiro/settings/` tree containing templates for the
three specification documents, templates for the three steering documents, and rules covering
matters such as EARS format and design principles. The directories for project context and for
per-feature specifications are not created at install time — each is created by the command that
first fills it, so a fresh installation contains only the settings tree.

## Capabilities

- Support for eight coding agents, selected by an installation flag, with two of them additionally
  offering a choice between a commands form and a subagents form.
- Specification output in thirteen languages, selected by a language flag, so that generated
  requirements and design documents can be produced in a language other than English.
- Two further installation flags: a dry-run that previews the changes without writing anything, and a
  backup that preserves existing files before overwriting them.
- A steering command that reads the codebase and generates three project-context files — product
  purpose, target users and core value; technology stack, version-control strategy and coding
  conventions; and directory structure patterns and naming conventions. These act as a project memory
  referenced by every other command, and re-running the command on a changed project detects the
  difference and proposes a synchronisation. It cannot run in an empty directory, because it works by
  analysing existing source.
- A requirements command that produces requirements in EARS format — Easy Approach to Requirements
  Syntax, a structured natural-language form using patterns such as "When…, the system shall…" to
  reduce ambiguity — answering what is to be built.
- A design command that answers how it is to be built, having the agent investigate the existing code
  and write an investigation log to one file before writing the technical design to another.
- A task-breakdown command that produces an implementation checklist, labelling each task as
  requiring sequential execution or permitting parallel execution so that the boundaries for
  concurrent work are explicit.
- An implementation command that can be pointed at a single task, at several tasks in sequence, or at
  every incomplete task.
- A validation command for checking consistency between updated specifications and tasks already
  completed, used when a requirement changes mid-implementation.
- A per-specification status field that is updated by hand on completion, which distinguishes
  in-progress specifications from finished ones.

## Adoption & Ecosystem

No adoption figures are recorded here. What is documented instead is how the tool is meant to be
used, and the guide that introduces it is emphatic on two points of practice. The flag that
auto-approves the previous phase should be avoided while learning the tool, because an error in the
requirements propagates into the design and the task breakdown together; and for a large feature,
tasks should be run one or two at a time with the agent's context cleared or compacted in between
(compare [[DefinedTerm/compaction]]) to keep its accuracy up. Both are that guide's author's
recommendation rather than documented tool behaviour.

The guide's own position is that specifications remain living documents, continuously updated
through development, rather than being frozen once implemented, and it records the recommendation
that completed specifications be committed to the repository rather than deleted — as a record
of design intent, as shared context that cannot be read off the code, as a reference for future
maintenance, and as context for reviewers. The recommended granularity is one specification per pull
request. Three kinds of work are named as unsuited to it: small fixes such as typos, tasks that a
single exchange settles, and exploratory work with no clear goal.
