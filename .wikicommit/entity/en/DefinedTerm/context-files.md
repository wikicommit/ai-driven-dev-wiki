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
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Markdown files that provide a central, machine-readable source of contextual information about the repository they sit in, loaded into an agentic AI coding tool's context every session. A February 2026 study of 2,926 GitHub repositories found them to be the dominant configuration mechanism for such tools, and often the only one a repository uses."
---

Context files are Markdown files that provide a central machine-readable source of contextual information about the repository in which they are used, loaded persistently into an agentic AI coding tool's context each session. [[ScholarlyArticle/configuring-agentic-ai-coding-tools]] characterises them as "READMEs for agents", carrying context-specific information such as build commands, coding conventions, and rules for CI/CD pipelines, and — like other configuration artifacts — version-controlled, inspectable, and collaboratively maintained.

## Usage

Each tool reads its own filename: CLAUDE.md for [[SoftwareApplication/claude-code]], `.github/copilot-instructions.md` and `.github/instructions/*.md` for [[SoftwareApplication/github-copilot]], [[DefinedTerm/agents-md]] (with AGENTS.override.md) for [[SoftwareApplication/codex-cli]], AGENTS.md and the now-deprecated `.cursorrules` for [[SoftwareApplication/cursor]], and GEMINI.md for [[SoftwareApplication/gemini-cli]]. Copilot additionally supports CLAUDE.md, AGENTS.md, and GEMINI.md.

In the study's sample of 2,926 repositories, context files were the most frequently adopted configuration mechanism by a wide margin, and in many cases a repository contained only a single context file artifact. The authors identified 4,860 context files across 2,634 repositories, with CLAUDE.md the most common file type at 1,661 files (34.2%), followed by AGENTS.md at 1,572 (32.3%) and copilot-instructions.md at 1,344 (27.7%); GEMINI.md (159 files, 3.3%) and `.cursorrules` (73, 1.5%) were rare. Measured by repository rather than file count, and against the 2,634 repositories that contain context files, CLAUDE.md appeared in 1,195 (45.4%), AGENTS.md in 1,069 (40.6%), and copilot-instructions.md in 925 (35.1%). Most repositories that use context files include only one or two of them.

Context files commonly refer to one another rather than duplicating content. The study identifies three reference patterns: a *direct pointer*, a single line naming another file via its filename, an imperative statement, or a Markdown link; a *short reference with context*, two to five lines saying what to do with the referenced file; and a *brief summary plus reference*, a header with one or two sentences of context followed by a pointer. Of 518 file pairs that reference each other, CLAUDE.md had the most outgoing references (357) and AGENTS.md the most incoming (368).

## Authoring guidance

Anthropic's Claude Code documentation gives the most explicit vendor guidance on writing one. Its recommended starting point is running `/init` to generate a starter file from the project structure and refining over time, and `/context` to confirm the file was loaded. There is no required format, but its central instruction is to keep the file short and human-readable, because the file is loaded every session and only things that apply broadly belong in it — domain knowledge or workflows relevant only sometimes belong in [[DefinedTerm/agent-skills]] instead, which load on demand.

The test it proposes for each line is: *"Would removing this cause Claude to make mistakes?"* If not, cut it. Its include/exclude table puts Bash commands the model cannot guess, code style rules that differ from defaults, testing instructions, repository etiquette, project-specific architectural decisions, environment quirks, and non-obvious gotchas on the include side; and anything the model can figure out from the code, standard language conventions, detailed API documentation, frequently-changing information, long explanations, file-by-file descriptions, and self-evident practices such as "write clean code" on the exclude side.

Its stated failure mode is bloat. A file that is too long causes the model to ignore instructions because important rules get lost in the noise — so if the model keeps doing something despite a rule against it, the documentation's diagnosis is that the file is too long rather than that the rule is unclear, while a model asking questions the file already answers suggests ambiguous phrasing. The recommended treatment is to handle the file like code: review it when things go wrong, prune regularly, and test changes by observing whether behaviour actually shifts. Where an instruction must be followed without exception, it recommends converting it to a hook (see [[DefinedTerm/agent-hooks]]) rather than restating it more forcefully, though it does note that emphasis such as "IMPORTANT" or "YOU MUST" can improve adherence. Files can import others using `@path/to/import` syntax, and the documentation recommends checking the file into git so a team can contribute to it.

Practitioner writing converges on the same point from other directions. [[BlogPosting/agentic-engineering-surpasses-vibe-coding]] gives passing context explicitly through `CLAUDE.md` and `README.md` as one of its five principles. [[BlogPosting/context-engineering]] frames the always-loaded file as a way of sidestepping the memory-selection problem entirely — a narrow fixed set of files pulled in every time, functioning as procedural memory — naming `CLAUDE.md` for Claude Code and rules files for Cursor and Windsurf. [[TechArticle/effective-context-engineering-for-ai-agents]] describes the same behaviour as half of a hybrid retrieval strategy, with `CLAUDE.md` dropped into context up front while glob and grep retrieve everything else just in time.

## Related Terms

Context files sit alongside seven other configuration mechanisms catalogued in the same study — [[DefinedTerm/agent-skills]], [[DefinedTerm/subagents]], Commands, Rules, Settings, Hooks, and MCP servers — but are distinguished by being both the most widely adopted and the lowest-friction to author. The study observes that this dominance means configuration is currently used more as documentation than as automation.
