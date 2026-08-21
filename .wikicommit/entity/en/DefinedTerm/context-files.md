---
title: "context files"
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
    url: 'https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents'
    hash: sha256:e58798c5643b30ca530a752cac84c2b7315004f5d4ba198bc788db7696e765be
  - type: url
    url: 'https://www.langchain.com/blog/context-engineering-for-agents'
    hash: sha256:07e9475327ca11aeabb710cea3b419188e2ca4380d3cf4fd055291761f52fb8f
  - type: url
    url: 'https://arxiv.org/pdf/2511.12884'
    hash: sha256:76efb50fd6bc599d4c645aaa06af94e83bc6b60e90aba276e96846dab7b04058
  - type: url
    url: 'https://arxiv.org/pdf/2510.21413'
    hash: sha256:7909394fa333078b9020474426f99bd50bbd8d63bcee81ee63930892a2f363a1
  - type: url
    url: 'https://www.humanlayer.dev/blog/skill-issue-harness-engineering-for-coding-agents'
    hash: sha256:210c3b64f14464d0f411066d18a2164f9d8b5069812277a8a440cb571d86e3f1
  - type: url
    url: 'https://arxiv.org/pdf/2604.21744'
    hash: sha256:9f7862701079fdcc2025b4eb823bc28cb07820a6313b554d8637b079e666e6f8
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Markdown files that provide a central, machine-readable source of contextual information about the repository they sit in, loaded into an agentic AI coding tool's context every session. A February 2026 study of 2,926 GitHub repositories found them to be the dominant configuration mechanism for such tools, and often the only one a repository uses."
---

Context files are Markdown files that provide a central machine-readable source of contextual information about the repository in which they are used, loaded persistently into an agentic AI coding tool's context each session. [[ScholarlyArticle/configuring-agentic-ai-coding-tools]] characterises them as "READMEs for agents", carrying context-specific information such as build commands, coding conventions, and rules for CI/CD pipelines, and — like other configuration artifacts — version-controlled, inspectable, and collaboratively maintained.

## Usage

Each tool reads its own filename: CLAUDE.md for [[SoftwareApplication/claude-code]], `.github/copilot-instructions.md` and `.github/instructions/*.md` for [[SoftwareApplication/github-copilot]], [[DefinedTerm/agents-md]] (with AGENTS.override.md) for [[SoftwareApplication/codex-cli]], AGENTS.md and the now-deprecated `.cursorrules` for [[SoftwareApplication/cursor]], and GEMINI.md for [[SoftwareApplication/gemini-cli]]. Copilot additionally supports CLAUDE.md, AGENTS.md, and GEMINI.md.

In the study's sample of 2,926 repositories, context files were the most frequently adopted configuration mechanism by a wide margin, and in many cases a repository contained only a single context file artifact. The authors identified 4,860 context files across 2,634 repositories, with CLAUDE.md the most common file type at 1,661 files (34.2%), followed by AGENTS.md at 1,572 (32.3%) and copilot-instructions.md at 1,344 (27.7%); GEMINI.md (159 files, 3.3%) and `.cursorrules` (73, 1.5%) were rare. Measured by repository rather than file count, and against the 2,634 repositories that contain context files, CLAUDE.md appeared in 1,195 (45.4%), AGENTS.md in 1,069 (40.6%), and copilot-instructions.md in 925 (35.1%). Most repositories that use context files include only one or two of them.

Context files commonly refer to one another rather than duplicating content. The study identifies three reference patterns: a *direct pointer*, a single line naming another file via its filename, an imperative statement, or a Markdown link; a *short reference with context*, two to five lines saying what to do with the referenced file; and a *brief summary plus reference*, a header with one or two sentences of context followed by a pointer. Of 518 file pairs that reference each other, CLAUDE.md had the most outgoing references (357) and AGENTS.md the most incoming (368).

## What these files are actually like

Two studies characterise the artifact itself rather than the tooling around it, and each reaches its own conclusion about what kind of thing it is.

[[ScholarlyArticle/agent-readmes]] concludes it behaves less like documentation than like configuration. Analysing 2,303 files from 1,925 repositories, it states the point flatly: these are "not static documentation but complex, difficult-to-read artifacts that evolve like configuration code through frequent, small additions". Its maintenance evidence is that 67.0% of Claude Code files are modified across multiple commits, with GitHub Copilot at 59.8% and OpenAI Codex at 59.4%, in short rapid bursts of small incremental additions and negligible deletions. Length differs by tool independently of task complexity — GitHub Copilot files at a median 535.0 words and Claude Code at 485.0, both substantially longer than OpenAI Codex files — while structure converges on a shallow hierarchy anchored by a single H1 with H2 and H3 subsections. On readability the study is unflattering: many files fall into a "difficult" band the authors compare to high-school-level material.

Its content taxonomy of 16 instruction categories shows what developers actually put in them. Testing leads at 75.9%, followed by implementation details at 70.8% and architecture at 68.1%; about half contain a system overview, and 24.1% explicitly define the agent's role and responsibilities. The omission the authors emphasise is non-functional: security appears in 14.8% of files, performance in 14.5% and UI/UX in 8.7%, from which they conclude that developers use context files to make agents functional while providing "few guardrails to ensure that agent-written code is secure or performant".

[[ScholarlyArticle/context-engineering-for-ai-agents-in-open-source-software]] describes the same artifact differently — as "documentation for machines", a new form of documentation that developers now write and maintain — and reports from a smaller AGENTS.md-focused sample that its conventions are still in flux: no established content structure and wide variation in how context is expressed — descriptive, prescriptive, prohibitive, explanatory, or conditional. Its adoption figure is the sobering one: only 5% of the 10,000 mature repositories it scanned had adopted any of the four formats it looked for. Its framing of why the artifact is worth studying at all is that prompts are rarely preserved after generation, so versioned context files are a rare direct window onto real-world [[DefinedTerm/context-engineering]].

## Authoring guidance

Anthropic's Claude Code documentation gives the most explicit vendor guidance on writing one. Its recommended starting point is running `/init` to generate a starter file from the project structure and refining over time, and `/context` to confirm the file was loaded. There is no required format, but its central instruction is to keep the file short and human-readable, because the file is loaded every session and only things that apply broadly belong in it — domain knowledge or workflows relevant only sometimes belong in [[DefinedTerm/agent-skills]] instead, which load on demand.

The test it proposes for each line is: *"Would removing this cause Claude to make mistakes?"* If not, cut it. Its include/exclude table puts Bash commands the model cannot guess, code style rules that differ from defaults, testing instructions, repository etiquette, project-specific architectural decisions, environment quirks, and non-obvious gotchas on the include side; and anything the model can figure out from the code, standard language conventions, detailed API documentation, frequently-changing information, long explanations, file-by-file descriptions, and self-evident practices such as "write clean code" on the exclude side.

Its stated failure mode is bloat. A file that is too long causes the model to ignore instructions because important rules get lost in the noise — so if the model keeps doing something despite a rule against it, the documentation's diagnosis is that the file is too long rather than that the rule is unclear, while a model asking questions the file already answers suggests ambiguous phrasing. The recommended treatment is to handle the file like code: review it when things go wrong, prune regularly, and test changes by observing whether behaviour actually shifts. Where an instruction must be followed without exception, it recommends converting it to a hook (see [[DefinedTerm/agent-hooks]]) rather than restating it more forcefully, though it does note that emphasis such as "IMPORTANT" or "YOU MUST" can improve adherence. Files can import others using `@path/to/import` syntax, and the documentation recommends checking the file into git so a team can contribute to it.

Practitioner writing converges on the same point from other directions. [[BlogPosting/agentic-engineering-surpasses-vibe-coding]] gives passing context explicitly through `CLAUDE.md` and `README.md` as one of its five principles. [[BlogPosting/context-engineering]] frames the always-loaded file as a way of sidestepping the memory-selection problem entirely — a narrow fixed set of files pulled in every time, functioning as procedural memory — naming `CLAUDE.md` for Claude Code and rules files for Cursor and Windsurf. [[TechArticle/effective-context-engineering-for-ai-agents]] describes the same behaviour as half of a hybrid retrieval strategy, with `CLAUDE.md` dropped into context up front while glob and grep retrieve everything else just in time.

### Evidence that most of these files do not help

The strongest published check on whether context files earn their place reaches this wiki secondhand, through [[BlogPosting/skill-issue-harness-engineering-for-coding-agents]]. That post summarises an ETH Zurich study testing 138 agentfiles across a variety of repositories and reports its findings as: LLM-generated files actually *hurt* performance while costing over 20% more; human-written ones helped only about 4%; agents spent 14–22% more reasoning tokens processing context-file instructions, took more steps, and ran more tools without improving resolution rates; and codebase overviews and directory listings did not help at all, because agents discover repository structure on their own. The study itself has not been ingested here, so these figures are recorded as that post's characterisation of it rather than as the study's own text.

The post's reading is that the findings confirm the authoring guidance above rather than undermining it — each failure it identifies maps onto advice that team had already given: do not auto-generate the file, include as few instructions as reasonably possible, use progressive disclosure, and keep contents concise and universally applicable. It reports its own file is under 60 lines. That converges with the 200-line ceiling recommended for large codebases in [[PresentationDigitalDocument/claude-code-advanced-patterns]] and with the vendor guidance above that diagnoses ignored rules as a length problem rather than a phrasing one.

### A proposed layer above the project file

[[ScholarlyArticle/agentic-ai-assisted-coding-epistemic-grounding]] argues that the file types now in common use share a gap: a plan file carries user intent, a project context file carries project guidelines, and a `SKILL.md` carries a technique, but none of them "enforce domain-specific validity constraints" — rules that hold regardless of what this user, this project, or this technique wants.

Its proposal is a fourth, field-scoped layer, [[DefinedTerm/epistemic-grounding-document]], written and governed by a domain community rather than by the repository's owners. The ordering it sets out is by decreasing plasticity — session, project, technique, field — with each layer more stable and authoritative than the one below, so that field-scoped invariants constrain everything beneath them and "win any conflict with the plan or skills, not the other way around."

Two design details distinguish it from the files described above. Its content splits into Hard Constraints, which override all other contexts, and Convention Parameters, which merely warn — a strictness distinction the single-tier files here do not make. And its authority is claimed to come from provenance rather than location: because the rules are the domain community's consensus rather than an individual's preference, the paper argues they "resist being overridden by non-experts," which is the case it makes for the whole layer given that the person driving the agent may not be a domain expert. This is a proposal illustrated by a drafted example file and backed so far by a single-configuration, single-turn proof-of-principle test — six prompts each violating a Hard Constraint, run against an adversarial project context file that told the agent to ignore scientific validity. Its authors report compliance improving substantially but degrading “under explicit override instructions or weakened normative language,” and note that no agent scaffold implements the authority ordering natively; loading through the system prompt was the workaround they found most consistent.

## Related Terms

Context files sit alongside seven other configuration mechanisms catalogued in the same study — [[DefinedTerm/agent-skills]], [[DefinedTerm/subagents]], Commands, Rules, Settings, Hooks, and MCP servers — but are distinguished by being both the most widely adopted and the lowest-friction to author. The study observes that this dominance means configuration is currently used more as documentation than as automation.
