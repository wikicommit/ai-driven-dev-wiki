---
title: "AGENTS.md"
type: "schema:DefinedTerm"
lang: en
tags: [agents, agent-config, agent-safety, security]
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
  - type: url
    url: 'https://developer.nvidia.com/blog/mitigating-indirect-agents-md-injection-attacks-in-agentic-environments/'
    hash: sha256:12ff9c9af90eba6dbc268a3eab17b477eca5b0dc3c223d5537d795ba8b206089
  - type: url
    url: 'https://github.com/agentsmd/agents.md'
    hash: sha256:0ee1b448835cb629994773e13324b6175ac210907c372308c45f2d1313aaec43
  - type: url
    url: 'https://github.blog/news-insights/company-news/welcome-home-agents/'
    hash: sha256:3d6ec841322ac0387923d4793d10946b52ad17fdca90ec22708b55bf57feced1
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/62010/'
    hash: sha256:212b9942c34a29825737eb0d331e5cd97a885416e16beed5147f5f78e9074c63
  - type: url
    url: 'https://docs.github.com/en/copilot/concepts/agents/code-review'
    hash: sha256:5288bbf7e00b1255000a7c40ad0d7129e795426d5c72d9dc46584d8c359c2ce8
  - type: url
    url: 'https://engineering.mercari.com/en/blog/entry/20251030-taming-agents-in-the-mercari-web-monorepo/'
    hash: sha256:2be25eae3259d1a99d5bcb659f731c2564ffe64e94c6bf0ad803148e7fb2a464
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A markdown file, conventionally at a repository's root, injected into an AI coding agent's context on every turn: an open format giving a dedicated, predictable place for the project context and instructions an agent should work from. One widely cited argument holds that only facts an agent cannot discover by reading the code itself earn a line in it."
---

AGENTS.md is a markdown file, conventionally placed at the root of a repository, that gets loaded into an AI coding agent's context on every prompt to convey project-specific conventions and constraints. Common coding agents can auto-generate one via an `/init`-style command, which scans a codebase and produces a description of its directory structure, tech stack, and testing conventions.

The format's own project describes it in one line as "a simple, open format for guiding coding
agents", and glosses it as a README for agents: a dedicated, predictable place to provide context
and instructions to help AI coding agents work on a project. It is published from the
`agentsmd/agents.md` repository under an MIT license, alongside a website at <https://agents.md/>
explaining the project's goals, and the repository carries a technical charter. The minimal example
the project ships is a plain Markdown file with three `##` sections — dev environment tips, testing
instructions, and pull-request instructions — whose contents are concrete commands and conventions
(which package manager command to use, where the CI plan lives, a required title format, checks to
run before committing) rather than prose about the codebase.

## Origin and Naming

One adopter's account fills in how the file came to carry the name it has. [[BlogPosting/taming-agents-in-the-mercari-web-monorepo]] records a team finding the standard at a point when it was `AGENT.md`, singular — described there as an RFC proposed by Sourcegraph through its AmpCode project — and consolidating its existing Cursor and Claude rules into one such file, while the rest of the team wondered about that RFC's longevity. The post then reports that OpenAI secured the agents.md domain, which it describes as the only thing that had been holding the standard back from the plural wording, and which was also the filename OpenAI's own Codex had already been using. It credits OpenAI's backing with the standard gaining much more traction among the tools that team used, and the team adopted the pluralized form as its single source of truth. This is one team's account of what it observed as an adopter, not a participant's account of how the standard was designed, and the announcements it refers to are not themselves among this wiki's sources.

That post also describes a practical consequence of adopting it in a codebase that already had per-tool rule files: `CLAUDE.md` and many other rule files simply became symlinks to the main one, so the pre-existing formats kept working without the content being maintained twice.

## Usage

Cited research summarized in the source found that a human-authored `AGENTS.md` recording genuinely non-discoverable, operationally significant facts (e.g. "use `uv` for package management") measurably changed agent behavior and improved task success, while an auto-generated file — typically a codebase overview the agent could otherwise discover by reading the repository directly — was found to add cost without improving, and in some cases while reducing, task success. The source also describes an "anchoring effect": once a technology or pattern is mentioned in the file, it stays in context on every subsequent prompt, which can bias the agent toward it even where it is no longer the current convention.

Another post by the same author cites OpenAI's Codex documentation as recommending an `AGENTS.md` file to give an agent consistent expectations about which tests to run, lint rules, dependency policies, and documentation requirements — likened there to onboarding a new hire with a map of conventions before they start writing code. That post also frames updating `AGENTS.md` and related checklists as the final "retro" step of a repeatable orchestration loop, so the next run starts smarter ([[BlogPosting/your-ai-coding-agents-need-a-manager]]).

GitHub adopted the file as one configuration surface for custom agents in VS Code, announced
alongside [[SoftwareApplication/agent-hq]] (see [[BlogPosting/introducing-agent-hq]]). It describes
`AGENTS.md` files there as source-controlled documents for setting clear rules and guardrails —
its examples being "prefer this logger" and "use table-driven tests for all handlers" — and states
the point as shaping Copilot's behaviour without re-prompting it every time.

GitHub's documentation for [[SoftwareApplication/github-copilot-code-review]] places the file
among four customization surfaces and separates them by scope, which is the clearest vendor
statement this wiki holds on when *not* to use it. `.github/copilot-instructions.md` holds
repository-wide always-on rules specific to Copilot; path-specific `*.instructions.md` files under
`.github/instructions/` hold always-on rules for particular paths, file types or directories;
`AGENTS.md`, read from the repository root, holds always-on rules meant to be shared across AI
tools and agents; and skills under `.github/skills/` hold task-specific workflows run on demand or
when relevant. GitHub compresses the distinction into four rules of thumb — "Copilot, always know
this for this repository", "Copilot, always know this when working in these paths", "Any agent,
always know this", and "Do this when needed" — so what marks `AGENTS.md` out on this account is
not scope within the repository but reach across tools, the same property the adopter account
above was choosing it for. The same documentation states that during a pull request review Copilot
reads custom instructions, agent instructions and skills from the head branch rather than the
base branch, so a change to any of them can be tested in the pull request that introduces it
without being merged first.

[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] discusses project-level configuration files such as `CLAUDE.md`, `.clinerules`, and `AGENT.md` as an early, grassroots practice of loading "institutional knowledge" before every agent task — codifying style guides, architectural constraints, and lessons learned into a continuously improving "employee handbook" for AI teammates. It frames this practice as an early example of what it proposes formalizing as [[DefinedTerm/mentorscript]], and states the community has no consensus on what such files should contain or the appropriate level of detail, arguing that future work involves not only defining more formal languages for this purpose but also discovering best practices for these files' effective use.

A practitioner account puts the file to a use none of the others describes at this depth: not only
as context the agent reads, but as the place whole *procedures* live.
[[BlogPosting/human-intent-ai-implementation-codex-workflow]] writes `AGENTS.md` at project
initialization as what it calls the AI's memory, holding the project overview, the folder layout,
the documents that must be consulted, the working rules and the current status. The four working
rules that post records in it are plan before acting and execute after approval, present three
options when planning or proposing, check and update the relevant specification before
implementing, and update the per-story context file on completion. Alongside those it stores the
auto-generation rules themselves — the phrases that trigger a routine, the steps to run, the
folder and file layout to produce, and the shape of the files that result. The consequence it
claims is on the prompt rather than on the agent: because placement and procedure are already
written down, a prompt can state a requirement ("read `vision.md` and generate the user stories")
instead of enumerating output paths, and the author's stated rule of thumb is that the more these
rule files are filled in, the simpler the prompts get and the better the output. That is one
engineer's demonstration on a sample project, with no measurement behind it.

## When It Applies

The source frames a good `AGENTS.md` as a living record of codebase friction rather than a permanent configuration: a line is added when an agent repeatedly makes the same mistake, and removed once the underlying problem (a confusing directory structure, a build pipeline that should catch something automatically) has been fixed instead. It states the practical filter as: if the agent could discover a fact by reading the code, it doesn't belong in the file. The source also treats a single, static, repository-root file as a structural limitation for any codebase past a certain complexity, since a flat instruction set cannot condition its content on what kind of task is being run, and proposes a hierarchy of directory- or module-scoped files, automatically maintained, as the intended replacement. It further describes a more elaborate three-layer version of this idea (a minimal routing file, task-scoped skill files, and a maintenance subagent), noting that no major coding agent yet exposes the lifecycle hooks needed to build that fuller architecture cleanly.

**This wiki's sources do not agree on what belongs in the file.** The first source above sets a discovery filter — a fact the agent could get by reading the code does not earn a line — which its author draws as the practical lesson of research finding an LLM-generated context file to reduce task success slightly while raising cost substantially. The practitioner account above stores the folder layout, the working rules and the auto-generation procedures in it, which is a good deal more than that filter would admit, and argues the opposite direction: that the fuller the rule files, the simpler the prompts and the better the output. The two are not measuring the same thing — one reports an experimental result about task success, the other one engineer's working method on a sample project — and neither engages the other, so both are recorded here rather than reconciled. What separates them may be purpose: a discovery filter is about what an agent needs to *know*, while procedures written to be triggered are about what it should *do*, which no amount of reading the code would supply.

One team has put something close to the hierarchy that first source proposes into practice, and its shape is worth recording because it sidesteps that disagreement rather than settling it. In [[BlogPosting/taming-agents-in-the-mercari-web-monorepo]] the root `AGENTS.md` holds almost nothing itself: each of its sections is a heading and a pointer to a separate document under `docs/` — build and test commands, code style and standards, project architecture, authentication patterns, testing strategy. The post singles out the architecture document as crucial given its repository's modular structure, and states the cost of omitting that context as most tools' output having to be completely restructured by the developer unless the same initial context is carefully prompted every time. It also teaches the agent the project's design system in emphatic ALWAYS/NEVER terms — always import components from the design system package rather than from source files, never add inline styles on a design system component or native HTML element — the stated reason being that the project must follow that design system and cannot rely on vibe-coded CSS.

That team's answer to keeping such files current is to delegate it: for any pull request with significant impact on higher-level design, an engineer runs an agent against the changeset together with the rules folder and has the model itself suggest edits to the rules, or point out inconsistencies in the code. Its stated reason for automating this is that editing a non-local markdown file in a separate folder is tedious for an engineer focused on a task, and it calls the result self-enforcing and self-updating documentation. That is the team's own characterization, offered without measurement, and what it was building at the time of writing — an agent on every pull request flagging code that diverges from the rules — had not yet shipped.

A later post on long-running agents gives the same file a further design principle for a developer running long or overnight coding jobs: treat `AGENTS.md` like a pilot's checklist, kept short, with every line earned by a real prior failure. It separately describes Anthropic's own scientific-computing agents using `CLAUDE.md` in a comparable role, as a living plan the agent itself edits as it learns, paired with a `CHANGELOG.md` acting as portable lab notes (see [[DefinedTerm/ralph-loop]]).

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

## Security Considerations

The property that makes the file useful is also what makes it a target. Because an agent loads these files as trusted project context by design, anything able to write one into the working tree can supply instructions carrying that standing. An NVIDIA AI Red Team report demonstrated this against Codex: a malicious Go dependency, executing during the build step as any dependency can, wrote an `AGENTS.md` whose directives claimed precedence over the user's own request, and the agent followed them in preference to the task it had been given. The report is explicit that the file's trust model is deliberate rather than a flaw, and that the attack presupposes a compromised dependency — which already implies code execution — so what it adds is a new use for that access rather than a new way to obtain it.

Among the mitigations it proposes, those aimed at the file itself are about its integrity rather than its content: limit which files an agent may read and write, enforce integrity controls on configuration files specifically, using endpoint security or centralized configuration management, and alert on unexpected file modifications. It proposes others that are not about the file at all — pinning exact dependency versions and scanning packages, auditing agent-generated pull requests with dedicated security agents, and scanning and guardrailing the model itself. See [[DefinedTerm/indirect-agents-md-injection]] for the attack itself.

This bears on the precedence rule described above. The codex-1 spec states that direct system, developer or user instructions outrank the file; in the reported attack the agent nonetheless acted on a file whose directives claimed the opposite, so that ordering is a documented default rather than something an injected file cannot contest.

## Related Terms

[[DefinedTerm/harness-engineering]], [[DefinedTerm/agentic-context-engineering]], [[DefinedTerm/ralph-loop]], [[DefinedTerm/indirect-agents-md-injection]], [[DefinedTerm/indirect-prompt-injection]], [[SoftwareApplication/openai-codex]]
