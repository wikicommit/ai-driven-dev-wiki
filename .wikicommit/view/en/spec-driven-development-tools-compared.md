---
title: "Spec-driven development tools compared"
lang: en
kind: comparison
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
derived_from:
  - path: .wikicommit/entity/en/SoftwareApplication/github-spec-kit.md
    source_commit: 74c6840463d960cf5b82c76818ec6b07f5f7233d
  - path: .wikicommit/entity/en/SoftwareApplication/kiro.md
    source_commit: 4b83a0390f0437f8f63f9399a1db3e12e1ace784
  - path: .wikicommit/entity/en/SoftwareApplication/tessl.md
    source_commit: 4b83a0390f0437f8f63f9399a1db3e12e1ace784
  - path: .wikicommit/entity/en/SoftwareApplication/openspec.md
    source_commit: 0ea12caf5df433486d9ab0e30d7c6a7b7cf57315
  - path: .wikicommit/entity/en/SoftwareApplication/spec-kitty.md
    source_commit: 0ea12caf5df433486d9ab0e30d7c6a7b7cf57315
  - path: .wikicommit/entity/en/SoftwareApplication/bmad.md
    source_commit: abe7dbaa9cb573068b927bda52cc565d6ba058e6
  - path: .wikicommit/entity/en/SoftwareApplication/get-shit-done.md
    source_commit: 0ea12caf5df433486d9ab0e30d7c6a7b7cf57315
  - path: .wikicommit/entity/en/SoftwareApplication/cc-sdd.md
    source_commit: 918f7af409eaecc35e50dea8e21fc3277faf15bf
  - path: .wikicommit/entity/en/DefinedTerm/spec-driven-development-levels.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/DefinedTerm/six-dimension-process-taxonomy.md
    source_commit: 0ea12caf5df433486d9ab0e30d7c6a7b7cf57315
---

Several tools in this wiki put [[DefinedTerm/spec-driven-development]] into practice: a written
specification comes between the developer's request and the coding agent's implementation. Each one
places that specification differently. This page sets eight of them side by side:
[[SoftwareApplication/github-spec-kit]], [[SoftwareApplication/kiro]], [[SoftwareApplication/tessl]],
[[SoftwareApplication/openspec]], [[SoftwareApplication/spec-kitty]], [[SoftwareApplication/bmad]],
[[SoftwareApplication/get-shit-done]] and [[SoftwareApplication/cc-sdd]]. It uses the two comparative
frames the wiki holds for this area. The page records where the tools differ. It does not say which
one to use.

## Two frames the wiki already holds

The wiki holds two instruments that compare these tools, and each has been applied to a different
subset of them.

- **Böckeler's implementation levels**, described in [[DefinedTerm/spec-driven-development-levels]],
  ask what happens to the spec after the task. In *spec-first* the spec is written for the task at
  hand. In *spec-anchored* it is kept and evolved with the feature. In *spec-as-source* the human
  edits only the spec and never the code. She applied the levels to Kiro, Spec Kit and Tessl as of
  late 2025.
- **The [[DefinedTerm/six-dimension-process-taxonomy]]** scores support frameworks from 0 to 2 on six
  dimensions: specification, context, roles, execution, validation and portability. Its study,
  [[ScholarlyArticle/from-prompt-to-process]], applied it to six frameworks. Five of them appear on
  this page: Spec Kit, OpenSpec, Spec Kitty, BMAD and GSD. A single rater scored each framework from
  its official documentation. The study states that the scores are the author's judgement rather
  than an independent empirical measurement.

The grounding pages record no six-dimension scores for Kiro, Tessl or cc-sdd, and Böckeler's levels
were not applied to cc-sdd.

## What the spec is to the code

On this axis the tools differ most sharply.

- **Tessl** sits at the spec-as-source end. There the specification is the only artifact developers
  edit, and the code is regenerated from it. Generated code carries a
  `// GENERATED FROM SPEC – DO NOT EDIT` marker. A documented command also works in reverse and
  derives a specification from existing code. Böckeler reads it as the only one of the three tools
  she examined that explicitly aims to be spec-anchored and explores spec-as-source.
- **Spec Kit** is presented by GitHub as a move from "code is the source of truth" to "intent is the
  source of truth". Böckeler nevertheless reads it as still spec-first only, because it creates a
  branch per spec.
- **Kiro** is read by Böckeler as mostly spec-first.
- **cc-sdd** takes an explicitly different stance in its version 3.0 README. The spec is a contract
  between parts of the system, the code remains the source of truth, and the spec makes the
  boundaries explicit so that humans and agents can work in parallel. Its introductory guide still
  treats specs as living documents that are committed rather than deleted once implemented.

## The shape of the process

| Tool | Documented flow |
|---|---|
| Kiro | Requirements → Design → Tasks, before any code generation |
| Spec Kit | Specify → Plan → Tasks → Implement → Converge, with implement and converge repeated until "Converged". Bug fixing and idea assessment are separate, opt-in entry points |
| Spec Kitty | spec, plan, tasks, next, review, accept, merge |
| cc-sdd | Steering, EARS-format requirements, design, task breakdown and implementation (command form). Version 3.0 adds a discovery entry point and long-running autonomous implementation |
| BMAD | Optional analysis, planning, solution and implementation phases, with a quick flow for smaller tasks. Its README describes entry points at Clarify, Plan or Build and verify |
| OpenSpec | One unified specification plus traceable change proposals, instead of a progression of separate documents |
| GSD | A layer of commands and conventions that turns broad requests into specifications and executable steps |
| Tessl | The spec is edited, and code is generated and regenerated from it |

One lineage between these flows is recorded. cc-sdd attributes its design to inspiration from
Kiro's spec-driven development and is compatible with Kiro specifications. It installs its templates,
including ones for three steering documents, under a `.kiro/settings/` tree. Kiro itself keeps its
Steering files under `.kiro/steering/`.

## Roles, context and validation

The six-dimension scores for the five frameworks the study assessed:

| Framework | Spec | Context | Roles | Execution | Validation | Portability | Total |
|---|---|---|---|---|---|---|---|
| BMAD | 2 | 2 | 2 | 1 | 2 | 1 | 10 |
| GSD | 1 | 2 | 0 | 1 | 0 | 0 | 4 |
| OpenSpec | 2 | 1 | 0 | 1 | 0 | 2 | 6 |
| Spec Kit | 2 | 1 | 1 | 1 | 1 | 2 | 8 |
| Spec Kitty | 2 | 1 | 1 | 2 | 2 | 1 | 9 |

The study reads a structural opposition between process depth and portability out of its table. The
frameworks scoring 2 on portability, Spec Kit and OpenSpec, give up roles and validation. The deepest
process, BMAD, gives up portability and execution. The framework most focused on context, GSD, scores
zero on roles, validation and portability. Specification scores 2 for almost every framework, so the
study treats it as the dimension that discriminates least. Roles and validation are the most
polarised, so they discriminate most.

The tools reach those scores by different means:

- **Roles.** BMAD takes the team metaphor literally. Its default agents are analyst, product
  manager, architect, developer, UX designer and technical writer, and each role triggers workflows
  that feed the next phase. OpenSpec and GSD score zero here.
- **Execution and isolation.** Spec Kitty isolates each work package in a
  [[DefinedTerm/git-worktrees|git worktree]] and requires review and acceptance before the merge. It
  is the only assessed framework scoring 2 on execution. cc-sdd v3.0 gives each task a fresh
  test-first implementer and an independent reviewer where the host agent has native subagents.
- **Context.** GSD treats context assembly as an explicit engineering task: what the agent reads, in
  what order and under which framing. Kiro's Steering files and cc-sdd's steering command give the
  agent standing project context in a different form: files describing product, technology and
  structure.
- **Human gates.** Spec Kit presents each phase as reviewed by a human before the next begins, and
  its repository insists that the skills be invoked one at a time. cc-sdd's own summary is that
  agents write the spec and humans approve the contract at phase gates. Its guide advises against
  the flag that auto-approves the previous phase while learning the tool.

## Portability and packaging

The tools bind to agents in different ways.

- **Spec Kit** is wired to one agent per project with `specify init --integration`. It runs its
  processes as `/speckit-*` agent skills and offers a `generic` integration for agents not listed.
- **OpenSpec** states support for dozens of code assistants through slash commands. The study reads
  this as positioning it as a thin layer over the agent.
- **cc-sdd** lists eight supported agents, two stable and six beta. It cautions that installing its
  skills does not verify that a host can run the full autonomous loop.
- **BMAD** installs as [[DefinedTerm/agent-skills]] or as a Claude Code or Codex plugin, and also
  packages selected workflows as Gemini Gems and ChatGPT Custom GPTs for planning outside a coding
  tool.
- **Spec Kitty** works with several agents but depends on its own repository conventions and on git
  worktrees.
- **GSD** is built for [[SoftwareApplication/claude-code]], and the study describes its portability
  as more limited than Spec Kit's or OpenSpec's.
- **Kiro** is a standalone AI IDE rather than a layer over another agent.

## What the sources caution

Each tool comes with its own caution in the grounding pages. These are the concerns the sources
raise, not verdicts.

- **Spec Kit:** drift between artifacts and implementation where validation is weak.
- **OpenSpec:** low overhead may fall short when a project needs more elaborate roles, architecture
  and validation.
- **Spec Kitty:** traction that is still modest, which leaves maturity and adoption open.
- **BMAD:** process cost, and the discipline needed to use it.
- **GSD:** dependence on a team's prompt conventions, and the volatility of a repository that
  signalled a move to a new organisation.
- **Kiro:** one handbook calls it intuitive but cumbersome and suited to one-off tasks, as an
  unmeasured judgement.
- **Tessl:** spec-as-source requires mature, trusted code-generation tooling. Böckeler wonders
  whether spec-as-source could inherit the downsides of both model-driven development and LLMs.
- **cc-sdd:** its guide names small fixes, single-exchange tasks and exploratory work as unsuited
  to it.

The taxonomy's study notes that most of the frameworks it was built for had not been through
independent academic evaluation. The Spec Kit, OpenSpec and BMAD pages each record this for their own
framework. The frameworks are under active development, so both classifications are snapshots.
