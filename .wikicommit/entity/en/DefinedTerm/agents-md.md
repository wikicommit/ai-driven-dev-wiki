---
title: "AGENTS.md"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/agents-md/'
    hash: sha256:ee43d2eb32e588d7c7bbadd7d7913c23bca92a53f6a8f01113bcb23e8b12d029
  - type: url
    url: 'https://addyosmani.com/blog/coding-agents-manager/'
    hash: sha256:fc697c3fcc830075a1a6b6751a1f242d4b6ff4ea9a385c1ec60a0c6f8a6e50a1
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
  - type: url
    url: 'https://openai.com/index/introducing-codex/'
    hash: sha256:2eb8d6fdb2ff536487274af973fe01fefa7c639f4f5ae546a6739e3e516ba93c
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A markdown file, conventionally at a repository's root, injected into an AI coding agent's context on every turn to record project conventions and non-obvious facts the agent cannot discover by reading the code itself."
---

AGENTS.md is a markdown file, conventionally placed at the root of a repository, that gets loaded into an AI coding agent's context on every prompt to convey project-specific conventions and constraints. Common coding agents can auto-generate one via an `/init`-style command, which scans a codebase and produces a description of its directory structure, tech stack, and testing conventions.

## Usage

Cited research summarized in the source found that a human-authored `AGENTS.md` recording genuinely non-discoverable, operationally significant facts (e.g. "use `uv` for package management") measurably changed agent behavior and improved task success, while an auto-generated file — typically a codebase overview the agent could otherwise discover by reading the repository directly — was found to add cost without improving, and in some cases while reducing, task success. The source also describes an "anchoring effect": once a technology or pattern is mentioned in the file, it stays in context on every subsequent prompt, which can bias the agent toward it even where it is no longer the current convention.

A later post by the same author cites OpenAI's Codex documentation as recommending an `AGENTS.md` file to give an agent consistent expectations about which tests to run, lint rules, dependency policies, and documentation requirements — likened there to onboarding a new hire with a map of conventions before they start writing code. That post also frames updating `AGENTS.md` and related checklists as the final "retro" step of a repeatable orchestration loop, so the next run starts smarter ([[BlogPosting/your-ai-coding-agents-need-a-manager]]).

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] discusses project-level configuration files such as `CLAUDE.md`, `.clinerules`, and `AGENT.md` as an early, grassroots practice of loading "institutional knowledge" before every agent task — codifying style guides, architectural constraints, and lessons learned into a continuously improving "employee handbook" for AI teammates. It frames this practice as an early example of what it proposes formalizing as [[DefinedTerm/mentorscript]], and states the community has no consensus on what such files should contain or the appropriate level of detail, arguing that future work involves not only defining more formal languages for this purpose but also discovering best practices for these files' effective use.

## When It Applies

The source frames a good `AGENTS.md` as a living record of codebase friction rather than a permanent configuration: a line is added when an agent repeatedly makes the same mistake, and removed once the underlying problem (a confusing directory structure, a build pipeline that should catch something automatically) has been fixed instead. It states the practical filter as: if the agent could discover a fact by reading the code, it doesn't belong in the file. The source also treats a single, static, repository-root file as a structural limitation for any codebase past a certain complexity, since a flat instruction set cannot condition its content on what kind of task is being run, and proposes a hierarchy of directory- or module-scoped files, automatically maintained, as the intended replacement. It further describes a more elaborate three-layer version of this idea (a minimal routing file, task-scoped skill files, and a maintenance subagent), noting that no major coding agent yet exposes the lifecycle hooks needed to build that fuller architecture cleanly.

A later post on long-running agents gives the same file a further design principle for a developer running long or overnight coding jobs: treat `AGENTS.md` like a pilot's checklist, kept short, with every line earned by a real prior failure. It separately describes Anthropic's own scientific-computing agents using `CLAUDE.md` in a comparable role, as a living plan the agent itself edits as it learns over a multi-day run, paired with a `CHANGELOG.md` acting as portable lab notes (see [[DefinedTerm/ralph-loop]]).

The most explicit statement of how such a file is actually interpreted comes from the vendor side.
OpenAI published the codex-1 system message as an appendix to [[BlogPosting/introducing-codex]], and
a section of it is an `AGENTS.md` spec written as rules the agent follows. It tells the agent that
these files can appear anywhere in the container's filesystem — typical locations being the root,
the home directory, and various places inside git repositories, so they need not live in a repo at
all; that a file's scope is the entire directory tree rooted at the folder containing it, and that
for every file touched in the final patch the agent must obey any `AGENTS.md` whose scope includes
it; that instructions about code style, structure and naming apply only within that scope unless
the file says otherwise; that a more deeply nested file takes precedence where instructions
conflict; and that direct system, developer or user instructions in the prompt outrank the file.
Two further provisions are about what the file can ask for rather than where it applies: any
programmatic checks it specifies must all be run, with a best effort to confirm they pass, after
all code changes and even for changes as simple as documentation; and instructions it gives about
pull-request messages are to be respected. OpenAI describes publishing the system message so that
developers can understand the model's default behaviour and tailor Codex to their own workflows,
and gives skipping those tests when short on time as an example of such a change — so the
precedence rule is presented as something a user can lean on, not only a conflict-resolution
detail.

## Related Terms

[[DefinedTerm/harness-engineering]], [[DefinedTerm/agentic-context-engineering]], [[DefinedTerm/ralph-loop]], [[SoftwareApplication/openai-codex]]
