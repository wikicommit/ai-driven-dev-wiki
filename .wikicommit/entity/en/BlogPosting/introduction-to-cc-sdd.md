---
title: "仕様から書くAI駆動開発へ ― cc-sdd 入門"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, coding-agents, agents, coding-tools]
sources:
  - type: url
    url: 'https://sreake.com/blog/learn-about-spec-driven-development/'
    hash: sha256:e8daa5b4df3be65a4f9ac7fc508f2c5e3a691b64fb7a69809011b0c17c3dba37
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A Japanese-language introduction to cc-sdd, an npm package that installs a spec-driven development workflow into AI coding agents: why specifying first stops repeated regeneration from drifting, what each of its six steps produces, and which kinds of work the specification overhead is not worth paying for."
  author: ["Nakahara Kodai"]
  datePublished: "2026-05-29"
  publisher: "Sreake"
---

The post is written for someone who has not yet used [[SoftwareApplication/cc-sdd]], and it opens
with the failure it is meant to address rather than with the tool. Asking an agent for a large
feature in one go, it argues, goes wrong in three recurring ways: the person asking has only vaguely
articulated the requirement, so what comes back varies; repeated retries overflow the context and
the agent loses the thread; and the reasoning behind a design ends up only in the conversation log,
where nobody can follow it afterwards. Its argument is that the staged progression human teams use —
requirements, design, task breakdown, implementation — exists to avoid exactly these problems, and
applies unchanged when the collaborator is an agent: structure the specification in advance and the
agent can concentrate on implementing while the human reviews at each stage.

The middle of the post is a walkthrough. One command installs the package, placing slash commands
under the agent's command directory and templates and rule files under a `.kiro/` tree; the
directories for project context and per-feature specifications are created later by the commands
that fill them. Six steps follow, from an optional codebase-analysis step through specification
initialisation, requirements, technical design and task breakdown to implementation. The author
explains what each phase writes and is emphatic on one point of process: the flag that
auto-approves the previous phase should not be used while learning, because an error in the
requirements propagates through the design and the tasks together.

The last third is about what happens after the code is written, and about when not to use any of
this. Specifications are to be treated as living documents rather than frozen once implemented: the
post gives a table of which downstream artefacts must be regenerated for each kind of change, always
flowing upstream to downstream, and recommends committing completed specifications to the repository
for four stated reasons. It then names three cases where the overhead is not worth paying — typo-scale
fixes, one-off questions, and exploratory work with no clear goal — and offers a granularity rule of
one specification per pull request.

## Key Points

- The stated problem is not that agents write bad code but that under-specified requests produce
  varying output, overflow the context on retries, and leave design rationale only in the chat log.
- The post's central claim is that structuring the specification up front lets the agent concentrate
  on implementation while giving the human a review point at each stage.
- cc-sdd is described as an npm package that provides this staged process as a set of slash commands,
  keeping requirements, design and tasks as Markdown files in the repository.
- Its design is attributed to inspiration from [[SoftwareApplication/kiro]]'s spec-driven
  development, with compatibility with Kiro specifications stated as what makes Kiro's practices
  reusable.
- Installation is a single `npx` invocation with a flag naming the agent and a flag naming the output
  language; the post reports it placing slash commands in the agent's command directory and
  templates plus rule files under `.kiro/settings/`.
- The post recommends previewing with the dry-run flag before running for real, so one can see what
  will be created and where.
- The minimum workflow is six steps: an optional steering step, specification initialisation, then
  requirements, technical design, task breakdown and implementation, each invoked as its own command.
- The steering step is described as reading the codebase to generate three files — the product's
  purpose, target users and core value; the technology stack, version-control strategy and coding
  conventions; and directory structure patterns and naming conventions — which then act as a project
  memory referenced by all of the commands.
- Re-running the steering step on a changed project is reported to detect the difference and propose
  a synchronisation, and it is documented as unable to run in an empty directory because it analyses
  existing source.
- Requirements are generated in EARS format — the post glosses this as Easy Approach to Requirements
  Syntax, a structured natural-language form using patterns such as "When…, the system shall…" to
  reduce ambiguity.
- The design phase is reported to have the agent investigate the existing code and leave an
  investigation log in one file before writing the technical design in another, separating the record
  of what was found from the decision taken.
- Generated tasks carry a label distinguishing those that must run sequentially from those that can
  run in parallel, which the post presents as making the boundaries for concurrent development
  explicit.
- The author's strongest process recommendation is against the auto-approve flag for beginners, on
  the stated grounds that a mistake at the requirements stage carries through the design and tasks
  together.
- For large features the post recommends implementing one or two tasks at a time and clearing or
  compacting the context between them to keep the agent's accuracy up (compare
  [[DefinedTerm/compaction]]).
- The post's own position is that specifications are to be treated as living documents,
  continuously updated through development, rather than frozen once implemented.
- Corrections are to flow upstream to downstream: the post tabulates which artefacts need
  regenerating for a requirements change, a design change and a task change respectively, with a task
  change affecting nothing downstream.
- For a large requirement change mid-implementation it recommends pausing, updating the three
  artefacts in order, and checking consistency against already-completed tasks with a validation
  command before resuming.
- Completed specifications are recommended to be committed rather than deleted, for four stated
  reasons: recording design intent the way an architecture decision record does, sharing context that
  cannot be read off the code, giving future maintainers the original requirements, and giving
  reviewers the what and why of a change.
- Three cases are named as unsuited to the process: small fixes such as typos or a single trivial
  file change, tasks answered in one exchange such as diagnosing an error, and exploratory work whose
  goal is not yet clear.
- The granularity the post recommends is one specification per pull request, which it argues keeps
  the correspondence between specification and code change tractable.
- Three common stumbles and their remedies are listed: thin steering content, which is fixed by
  re-running the step and editing the files by hand; context overflow, fixed by per-task execution
  and clearing between tasks; and the steering step failing in an empty directory, which is fixed by
  running it in a project root that already has source code, since the step works by analysing it.

## Context

The post is an introductory guide published on a Japanese cloud-consultancy blog, and it presents
itself as such: its stated goal is that a reader finish it ready to run the installation command and
write a first specification, and its closing suggestion is a single lap through the workflow on a
small feature rather than wholesale adoption. Its authority is the tool's own documentation, which it links for command reference, the spec-driven
guide and customisation, alongside an article and a slide deck that it also links; the
details of those documents are theirs and are not established here. Where it goes
beyond description it is explicit about doing so — the warning against the auto-approve flag, the
one-specification-per-pull-request rule and the advice to clear context between tasks are offered as
the author's recommendations rather than as documented behaviour. The practice it teaches is treated
as its own subject, across many implementations, under [[DefinedTerm/spec-driven-development]].
