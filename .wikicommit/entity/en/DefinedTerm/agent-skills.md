---
title: "Agent Skills"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, configuration, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/html/2602.14690v1'
    hash: sha256:a95102e253d7131ba8bf5f38f7f1e738784be17159af65fa612395d8ed4800b9
  - type: url
    url: 'https://code.claude.com/docs/en/best-practices'
    hash: sha256:92807ef3d58f63fbea435ea928df49e2f3341e118eb8c40db08800c100a4c4c5
  - type: url
    url: 'https://github.com/NeoLabHQ/context-engineering-kit'
    hash: sha256:bc2a9a7e51d46faa7b71b485a040ec8d6f6b10a78fc25f17a65dc7b9dde39b4c
  - type: url
    url: 'https://code.claude.com/docs/en/skills'
    hash: sha256:0a1bf9dee2f0ff1bb9f2ab54bbdd859d458c6bc13d2159e42d3ced61ce360a94
  - type: url
    url: 'https://www.jfokus.se/jfokus26-preso/Spec-driven-Development-using-Coding-Agents.pdf'
    hash: sha256:826071b0039518cb28ef1798aa3d05619a61db6492c48424db207313c18d6363
  - type: url
    url: 'https://en.wikipedia.org/wiki/Model_Context_Protocol'
    hash: sha256:f114caf967b13aa97382a0bea6ed771c920c8c79930883437e9a34df46e9c542
  - type: url
    url: 'https://www.anthropic.com/engineering/code-execution-with-mcp'
    hash: sha256:00595274b94dc84401f5d20a982fac4221bd6fef1a8b89c318ac7ad3122afaf8
  - type: url
    url: 'https://github.com/agentskills/agentskills'
    hash: sha256:62d24fa3cf7cabfa0348af3065f32a15c43faf2d30b3352ff41f02e3a2399faa
  - type: url
    url: 'https://arxiv.org/pdf/2605.13044'
    hash: sha256:a0f563e8eab498ab940d491c23dbefca46144c318375cdb4d69d12a19fb5532f
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A configuration mechanism for agentic AI coding tools, referred to simply as Skills, that bundles prompts, tools, and documentation an agent can invoke on demand. Originally developed by Anthropic and released as an open standard, a Skill is a directory containing a SKILL.md file with metadata and instructions, loaded by agents through progressive disclosure."
---

Agent Skills — referred to in the literature simply as Skills — are a configuration mechanism that extends the capabilities of agentic AI coding tools with specialized contextual knowledge and workflows. [[ScholarlyArticle/configuring-agentic-ai-coding-tools]] describes them as bundling prompts, tools, and documentation that an agent can invoke on demand. They were introduced by Anthropic and now serve as an open standard supported across tools.

Structurally, a Skill is a directory containing a SKILL.md file. That file must include YAML frontmatter with at least a name and a description, followed by body instructions for how a task should be performed. Skills execute their instructions within the calling agent's own context, which is what distinguishes them from [[DefinedTerm/subagents]].

## Usage

All five tools surveyed in that study support Skills, each under its own directory: `.claude/skills/`, `.github/skills/`, `.codex/skills/`, `.cursor/skills/`, and `.gemini/skills/`.

A Skill can draw on three types of optional resource, loaded by the agent when required: `scripts/` for executable code the agent can run, with Python, Bash, and JavaScript among the language options; `references/` for documentation the agent can read on demand, including technical references, templates, or structured data; and `assets/` for static resources such as document and configuration templates, images, and data files.

Adoption in practice is shallow relative to that expressive range. The study found 601 Skills across 158 repositories, averaging 3.8 per repository but with a median of 2 (minimum 1, maximum 28). The vast majority — 501 Skills, or 83.3% — included no additional resources at all. Where resources were present, `references/` was most common (48 Skills, 8.0%), followed by `scripts/` (34, 5.7%); 12 Skills (2.0%) combined both, `assets/` appeared in only four (0.7%), and the remaining combinations occurred once each. The authors summarise this as Skills relying predominantly on static documentation rather than dynamic, executable resources, and conclude that in practice Skills function primarily as structured text rather than as executable workflow bundles.

Developers do appear to follow the specification's length guidance: it recommends keeping SKILL.md files under 500 lines and moving detailed material to separate files, and only 25 of the 601 Skills found (4%) exceeded that.

Anthropic's Claude Code documentation describes two distinct uses for the mechanism. The first is knowledge specific to a project, team, or domain, applied automatically when relevant — its example being an `api-conventions` skill holding REST design rules. The second is a repeatable workflow invoked directly as `/skill-name`, its example being a `fix-issue` skill whose body is a numbered procedure for analysing and fixing a GitHub issue; for workflows with side effects the documentation recommends `disable-model-invocation: true` so they only run when triggered deliberately. It also frames Skills against [[DefinedTerm/context-files]] on a loading criterion: a context file is loaded every session, so only broadly-applicable material belongs there, while knowledge relevant only sometimes belongs in a Skill that loads on demand without bloating every conversation.

Skills are also the packaging format for third-party distribution. [[SoftwareApplication/context-engineering-kit]] ships its techniques as plugins whose skills follow the agentskills.io specification, and its maintainers describe preferring command-oriented skills paired with subagents over general information skills, specifically to avoid populating context with information that will not be needed — a token-efficiency argument for the same on-demand property. They note the limitation that installing skills through generic tooling does not carry subagents across, so a plugin depending on both is only partially portable.

### The format as its own specification describes it

The Agent Skills specification repository states the format's purpose as "a standardized way to give AI agents new capabilities and expertise", and calls it "a lightweight, open format for extending AI agent capabilities with specialized knowledge and workflows". Its minimal definition matches the survey account above: a skill is a folder containing a `SKILL.md` file carrying metadata — `name` and `description` at minimum — plus instructions telling an agent how to perform a specific task, with optional bundled scripts, reference materials, templates and other resources.

The motivation it gives is a context gap: agents are increasingly capable but often lack the context needed to do real work reliably, and skills answer that by packaging procedural knowledge together with company-, team- and user-specific context into portable, version-controlled folders that agents load on demand. It names three resulting properties — domain expertise, in that specialized knowledge from legal review processes to data analysis pipelines to presentation formatting becomes reusable instructions and resources; repeatable workflows, in that multi-step tasks become consistent, auditable procedures; and cross-product reuse, in that a skill built once can be used across any skills-compatible agent.

Loading works by [[DefinedTerm/progressive-disclosure]] in three stages. At **discovery**, agents load only the name and description of each available skill at startup — just enough to know when it might be relevant. At **activation**, when a task matches a skill's description, the agent reads the full `SKILL.md` instructions into context. At **execution**, the agent follows those instructions, optionally running bundled code or loading referenced files as needed. Because full instructions load only when a task calls for them, the specification states that agents can keep many skills on hand with only a small context footprint.

On governance, the specification repository states that the format "was originally developed by [[Organization/anthropic]], released as an open standard, and has been adopted by a growing number of agent products", and that the standard is open to contributions from the broader ecosystem. Code in the repository is licensed under Apache 2.0 and its documentation under CC-BY-4.0. The repository points to `agentskills.io` for documentation and the format specification, and separately links to a Client Showcase at `agentskills.io/clients` as a way to explore some of the AI tools and agentic clients that support the format, which it says are a large number.

### The mechanism as one vendor documents it

Anthropic's dedicated Claude Code skills documentation sets out the mechanism in more detail than the survey above, and is explicit that what it documents is a superset: Claude Code skills follow the Agent Skills open standard published at agentskills.io, which the documentation describes as working across multiple AI tools, and Claude Code then extends that standard with features of its own — invocation control, running a skill in a subagent, and dynamic context injection. The boundary is enforced rather than advisory: outside Claude Code, only six frontmatter fields from the spec are accepted (`name`, `description`, `license`, `compatibility`, `metadata`, `allowed-tools`), and including any other field makes packaging or upload fail with a hard error rather than ignoring the field.

Two design points in that documentation bear on how the mechanism differs from a context file. The first is the loading criterion already noted above, stated there as a cost argument: a skill's body loads only when it is used, so long reference material costs almost nothing until it is needed. The second is what happens after it loads — the rendered `SKILL.md` enters the conversation as a single message and stays there for the rest of the session, so, in the documentation's framing, every line is a recurring token cost and guidance meant to apply throughout a task should be written as standing instructions rather than one-time steps. Auto-compaction carries invoked skills forward within a budget, re-attaching the most recent invocation of each skill after the summary, keeping the first 5,000 tokens of each within a combined 25,000-token budget filled from the most recently invoked skill first, so older skills can be dropped entirely in a session that invoked many.

The documentation splits skill content into two kinds by how it is meant to be triggered. **Reference content** — conventions, patterns, style guides, domain knowledge — runs inline so the model can apply it alongside the conversation. **Task content** — step-by-step instructions for deployments, commits, code generation — is usually meant to be invoked deliberately as `/skill-name`. Two frontmatter fields control which is possible: `disable-model-invocation: true` means only the user can invoke the skill, recommended for anything with side effects on the reasoning that you do not want the model deciding to deploy because the code looks ready; `user-invocable: false` means only the model can, for background knowledge that is not a meaningful action for a user to take.

Beyond those, the documented frontmatter covers argument handling (`arguments`, `argument-hint`), model and effort overrides that apply while the skill is active, `paths` globs that limit when a skill activates automatically, `hooks` that the skill registers when invoked (see [[DefinedTerm/agent-hooks]]), and `context: fork`, which runs the skill in a forked subagent context instead of inline — the one documented case where a skill does *not* execute in the calling agent's context. `allowed-tools` pre-approves tools for the turn that invokes the skill, and the documentation flags this as a supply-chain concern in its own right: workspace trust does not gate the field, so a skill checked into a repository can grant itself broad tool access, and it recommends reviewing the `allowed-tools` of repository skills before running the agent there.

Where a skill file lives determines who can use it, and name collisions resolve by source rather than by proximity: enterprise overrides personal, personal overrides project, and a skill at any of those levels overrides a bundled skill of the same name — though not that bundled skill's aliases. Plugin skills sit in a `plugin-name:skill-name` namespace and so do not conflict with skills at the other levels. Skills also load from nested `.claude/skills/` directories below the working directory, becoming available the first time the agent reads or edits a file in that subdirectory, which lets a package inside a monorepo supply skills scoped to itself.

Claude Code also ships a set of **bundled skills** — the documentation names `/doctor`, `/code-review`, `/batch`, `/debug`, `/loop`, and `/claude-api` — which it describes as prompt-based, giving the model detailed instructions and letting it orchestrate the work with its own tools, in contrast to most built-in commands, which execute fixed logic directly. Some are invoked automatically when relevant; others run only on explicit invocation, which the documentation justifies as keeping the user in control of when longer-running checks spend time and tokens.

### Skills as portable engineering practice

[[Person/arun-gupta]]'s [[PresentationDigitalDocument/spec-driven-development-using-coding-agents]] argues for the mechanism on reuse grounds rather than context grounds, describing skills as portable engineering patterns: capture a solution once and apply it across multiple projects and agents, codifying best practices as versioned skills instead of reinventing prompts per project. The categories he names are testing patterns, API integration, deployment scripts, code review guidelines, and infrastructure-as-code, with a Helm skill given as the example of enforcing a consistent approach to writing Helm charts. He points at the `agentskills.io` specification and at a skill repository for discovering, sharing and contributing reusable agent capabilities.

The connection he draws to [[DefinedTerm/spec-driven-development]] is that the two reinforce each other: specifications reference standardized skills, which makes the specifications themselves more precise and actionable, while the skills reduce prompt engineering overhead. His worked example is a skill that implements one sub-section of an implementation plan end to end — starting from a clear context to avoid context pollution, reading the requirements out of the plan, creating task tracking, implementing to project patterns, writing tests, running quality checks that must pass, updating documentation, and committing — with the skill body referencing other skills by name for error handling, API endpoint implementation, test writing, and commit format.

### As a companion standard to MCP

The Wikipedia account of [[DefinedTerm/model-context-protocol]] dates Anthropic's publication of Agent Skills to December 2025, describing it as a companion open standard for packaging task-specific instructions and resources that AI agents load on demand, following the same open-standard approach as MCP — the same month Anthropic donated MCP itself to the [[Organization/agentic-ai-foundation]].

Anthropic's own engineering writing reaches skills from a different direction. [[TechArticle/code-execution-with-mcp]] describes them as folders of reusable instructions, scripts and resources for models to improve performance on specialized tasks, and treats them as the natural endpoint for an agent with filesystem access: once an agent has developed working code for a task it can save that implementation for future use, and adding a `SKILL.md` file to such a saved function creates a structured skill the model can reference. On that account the agent gradually builds a toolbox of higher-level capabilities, evolving the scaffolding it needs to work most effectively — see [[DefinedTerm/code-execution-with-mcp]].

### The safety rules skills declare for themselves

Because a skill bundles natural-language instructions with optional executable scripts, its safety constraints are written as prose rather than enforced by a runtime — and [[ScholarlyArticle/no-attack-required]] reports that those constraints frequently do not hold. Its semantic fuzzing of 402 skills from the OpenClaw marketplace found [[DefinedTerm/specification-violations]] in 120 of them (29.9%), including 26 previously unknown exploitable guardrail violations in deployed skills. The failures it describes need no attacker: an ordinary user request causes a skill to breach a rule its own specification declared.

Two of its findings bear directly on how skills are written. The first is that clear prose is not sufficient — of the 120 violated skills, 46 (38%) had all their guardrails rated well-written by an independent LLM judge, and were violated anyway because terms such as "critical domains" and "explicit approval" have no runtime definition. The second concerns the execution environment: skill specifications are typically written for human-interactive use or CI/CD automation, while agent execution is a third modality with no stdin yet a reachable human, so confirmation prompts built on shell or `input()` reads fail silently and push the agent toward `--yes` and `--force` flags that bypass the intended gate. The paper's recommendation to skill authors is that guardrails "must be operationally testable, not probabilistically interpreted".

## Related Terms

Skills are one of eight configuration mechanisms catalogued in the study, alongside [[DefinedTerm/context-files]], [[DefinedTerm/subagents]], Commands, Rules, Settings, Hooks, and MCP servers (see [[DefinedTerm/model-context-protocol]]). The authors argue Skills offer untapped potential for encoding recurring workflows beyond static instructions, and suggest the gap between that potential and current usage reflects both the mechanism's recency and the design and maintenance effort executable Skills require compared with authoring Markdown instructions.
