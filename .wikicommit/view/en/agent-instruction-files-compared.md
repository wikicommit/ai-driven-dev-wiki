---
title: "Agent instruction files compared"
lang: en
kind: comparison
review_status: pending
generated_at: "2026-09-26"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
derived_from:
  - path: .wikicommit/entity/en/DefinedTerm/agents-md.md
    source_commit: 07f44d78c36c0f3ef8211927eac4fa818f178ac1
  - path: .wikicommit/entity/en/DefinedTerm/claude-md.md
    source_commit: 8e44cc8042b43f8d5552cfe8212a0f427fe92366
  - path: .wikicommit/entity/en/DefinedTerm/agent-md.md
    source_commit: abe7dbaa9cb573068b927bda52cc565d6ba058e6
  - path: .wikicommit/entity/en/DefinedTerm/design-md.md
    source_commit: 07f44d78c36c0f3ef8211927eac4fa818f178ac1
  - path: .wikicommit/entity/en/DefinedTerm/ai-ide-rules.md
    source_commit: 07f44d78c36c0f3ef8211927eac4fa818f178ac1
  - path: .wikicommit/entity/en/DefinedTerm/memory-bank.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/DefinedTerm/mentorscript.md
    source_commit: 1241f6026eea3b9fe7666601cd9fbf68d202989f
  - path: .wikicommit/entity/en/BlogPosting/division-of-labor-in-ai-instruction-files.md
    source_commit: 07f44d78c36c0f3ef8211927eac4fa818f178ac1
  - path: .wikicommit/entity/en/ScholarlyArticle/on-the-impact-of-agents-md-files-on-the-efficiency-of-ai-coding-agents.md
    source_commit: 864e0a92b6b7213d87ef534b8204d9992ffc5386
  - path: .wikicommit/entity/en/BlogPosting/stop-using-init-for-agents-md.md
    source_commit: 908ab492691e9fcd622bfa73c6c2fd839716bea1
---

Several file formats in this wiki do the same basic job: they hold text that a coding agent loads as
standing context, so that a project's conventions do not have to be re-typed every session. They
differ in which tools read them, where they live, when they load, and what they are meant to hold.
This page sets seven of them side by side — [[DefinedTerm/agents-md]], [[DefinedTerm/claude-md]],
[[DefinedTerm/agent-md]], [[DefinedTerm/ai-ide-rules]], [[DefinedTerm/design-md]],
[[DefinedTerm/mentorscript]] and the umbrella term [[DefinedTerm/memory-bank]] — and then turns to
what the evidence held here says about their content. It draws out differences and does not rank
the formats.

## Side by side

| Format | Read by | Where it lives and how far it reaches | What it is meant to hold | Standing |
|---|---|---|---|---|
| `AGENTS.md` | Any agent that supports it; the format's project calls it a README for agents | Conventionally the repository root; the codex-1 system message lets it appear anywhere, applying to the directory tree below it, with a more deeply nested file taking precedence | Concrete commands and conventions — the project's minimal example has dev environment tips, testing instructions and pull-request instructions | Open format published under MIT; described as donated to the Linux Foundation in December 2025 |
| `CLAUDE.md` | Claude Code | Four scopes (managed policy, user, project, personal local); a root file loads at session start and is re-read after compaction, a subdirectory file loads when Claude reads a file there; files up the directory tree are concatenated rather than overriding each other | Standing project facts: build commands, directory layout, conventions, team norms | One vendor's product mechanism |
| `AGENT.md` | Amp natively; several other tools through symbolic links, per its specification | MUST sit at the project root; implementations SHOULD support a hierarchy including a user-global `~/.config/AGENT.md`, with more specific files taking precedence | Project structure, build/test commands, code style, architecture, testing, security | RFC-style specification dated July 2025, written for Sourcegraph |
| AI IDE rules | One IDE each — `.cursor/rules/`, `.windsurf/rules/`, `.trae/rules/`, `.qoder/rules/`, `.kiro/steering/` | A per-tool directory; one vendor's guide adds four trigger types (Manual, Model Decision, Always, Specific Files) and caps a file at 10,000 characters | Architectural constraints, coding style, library preferences, workflow | Per-tool product features, studied in one mining and survey study |
| `DESIGN.md` | An agent generating a user interface | A single file | Design-system tokens as machine-readable YAML, with the design intent in the Markdown body; ships with a `lint` and a `diff` command | Published by Google Labs in April 2026 |
| MentorScript | Agents in the proposed SASE framework | Version-controlled rulebook | Team norms, from granular checks to high-level principles, with each agent action traceable to the rules considered | A proposal in one paper, as part of the SASE framework |
| Memory bank | Any AI coding session in a codebase | Across all sessions, as opposed to per task | General context such as rules files and product or architecture descriptions — Kiro's "steering", Spec Kit's "constitution" | A name Birgitta Böckeler adopts to separate this context from specs |

## One role, several names

`AGENTS.md` and `AGENT.md` fill the same role and differ in name. The `AGENT.md` specification says
it prefers the singular because its authors own the agent.md domain and commit to keeping it
vendor-neutral, and that it is willing to compromise. One adopter's account records a team
consolidating onto `AGENT.md`, then switching to the plural after OpenAI secured the agents.md
domain. A later post describes the plural form as promoted jointly by OpenAI, Google, Cursor,
Factory and others before its donation to the Linux Foundation.

The same symbolic-link arrangement recurs across these accounts as the way to keep tool-specific
filenames working without maintaining the content twice. The `AGENT.md` specification gives
migration commands that move a tool's own file to `AGENT.md` and leave a link behind. One team made
`CLAUDE.md` and its other rule files links to its `AGENTS.md`. The post on
[[BlogPosting/division-of-labor-in-ai-instruction-files]] gives the format project's recommendation as
making `AGENTS.md` the real file and `CLAUDE.md` a link to it.

The grounding pages describe Claude Code's handling of `AGENTS.md` differently. The `AGENTS.md` page
records that post's statement that Claude Code reads `CLAUDE.md` and not `AGENTS.md`. The `CLAUDE.md`
page records Claude Code's documentation as saying it reads a repository's `AGENTS.md` by default
only when no `CLAUDE.md` or `CLAUDE.local.md` exists, with a setting to read both and `@AGENTS.md`
imports as the way to share one file. Both accounts are recorded here as each page gives them.

## When the content loads

The formats differ in how a file comes into context, and in what happens when two files disagree:

- **Directory scope with nesting.** The codex-1 system message scopes an `AGENTS.md` to the directory
  tree containing it, gives the more deeply nested file precedence, and ranks direct system,
  developer or user instructions above the file. The `AGENT.md` specification likewise asks that
  more specific files take precedence over general ones.
- **Concatenation.** Claude Code's documentation says `CLAUDE.md` files found up the directory tree
  are concatenated rather than overriding one another, so instructions closer to where Claude was
  launched are read last. Rules under `.claude/rules/` load at launch unless a `paths` field limits
  them to matching files.
- **Trigger types.** Alibaba Cloud's guide for Lingma sorts rules by how they are triggered — by name
  in the chat, by the model deciding a rule's description fits, on every request, or by file glob —
  and states that where a rule and the assistant's memory conflict, the rule takes precedence.
- **Organisation-wide policy.** Claude Code's managed `CLAUDE.md`, deployed through MDM or
  configuration management, cannot be excluded by individual settings.

## Splitting by subject

Two framings split this context by what it covers rather than by which tool reads it.
[[BlogPosting/division-of-labor-in-ai-instruction-files]] reads the files as three non-overlapping
layers: `AGENTS.md` (with `CLAUDE.md` as its tool-specific equivalent) for an agent's premises, roles
and prohibitions, `SKILL.md` for reusable tasks, and `DESIGN.md` for appearance. It places each layer
differently on a machine-readable/human-readable axis — `AGENTS.md` almost entirely prose, `SKILL.md`
structuring only its leading YAML, `DESIGN.md` separating tokens from intent — and offers the split
as an option to adopt where it earns its place rather than a target state.

The memory-bank framing draws its line along time instead: memory bank files are relevant to every
session in a codebase, specs only to the tasks that change the functionality they describe. The
three-layer post makes a similar distinction, describing a spec-driven development spec as archived
once its feature is done, while the three layers describe standing norms that are maintained and
grow.

## What belongs in the file

The pages record different answers to what such a file should contain:

- **A discovery filter.** [[BlogPosting/stop-using-init-for-agents-md]] argues that a fact the agent
  could discover by reading the code does not belong in the file, and that an auto-generated codebase
  overview is redundant. It also describes an anchoring effect: a technology mentioned in the file
  stays in context on every prompt and can bias the agent toward an outdated pattern.
- **Procedures in the file.** A practitioner account recorded on the `AGENTS.md` page stores the folder
  layout, working rules and auto-generation procedures in it, arguing that fuller rule files make for
  simpler prompts. The `AGENTS.md` page records the two positions without reconciling them.
- **Procedures out of the file.** Anthropic's guidance recorded on the `CLAUDE.md` page moves
  multi-step procedures to skills, part-of-the-codebase concerns to path-scoped rules, and anything
  that must always or never happen to hooks or permissions, because a prompted rule can fail to be
  followed.
- **Size.** Anthropic recommends keeping a `CLAUDE.md` under 200 lines. HumanLayer reports a general
  consensus that under 300 lines is best and keeps its own root file under sixty. Both are presented
  on the page as recommendations rather than measured thresholds.
- **No settled answer.** The paper proposing MentorScript states that the community has no consensus
  on what such files should contain or at what level of detail.

## What the evidence measures

Three studies bear on these files, and each measures something different:

- **Efficiency with and without `AGENTS.md`.**
  [[ScholarlyArticle/on-the-impact-of-agents-md-files-on-the-efficiency-of-ai-coding-agents]] ran
  OpenAI Codex on 124 pull-request tasks from 10 repositories with and without the root `AGENTS.md`.
  Median wall-clock time fell by 28.64% and median output tokens by 16.58%. The authors stress that
  this is not a correctness evaluation, and the study covers one agent and small code-only changes.
- **Task success by who wrote the file.** As reported in
  [[BlogPosting/stop-using-init-for-agents-md]], an ETH Zurich study found LLM-generated context files
  reduced task success by 2–3% while raising cost by over 20%, and developer-written files improved
  success by about 4% while raising cost by up to 19%. The post reconciles this with the efficiency
  study by what the file contains, not whether it exists.
- **What rule files contain and how well they are followed.**
  [[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]], as recorded on the AI IDE rules page,
  mined 7,310 rules from 83 projects. Architectural and context-management rules were rated most
  important but made up 2.67% and 1.76% of the rules. Updating a rule raised compliance by 22.99% on
  average, concentrated in concrete, statically checkable constraints, and compliance fell back toward
  65% over the following commits. Its projects are predominantly TypeScript web development by solo
  developers or teams of one to three.

The remaining formats rest on other kinds of standing: `AGENT.md` and MentorScript on proposals,
`DESIGN.md` on its publisher's specification and tooling, and `CLAUDE.md` on vendor documentation and
one outside company's recommendations.
