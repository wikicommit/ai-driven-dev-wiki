---
title: "AGENTS.md"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, configuration, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/html/2602.14690v1'
    hash: sha256:a95102e253d7131ba8bf5f38f7f1e738784be17159af65fa612395d8ed4800b9
  - type: url
    url: 'https://www.jfokus.se/jfokus26-preso/Spec-driven-Development-using-Coding-Agents.pdf'
    hash: sha256:826071b0039518cb28ef1798aa3d05619a61db6492c48424db207313c18d6363
  - type: url
    url: 'https://openai.com/index/introducing-codex/'
    hash: sha256:c899f94e6c00781777e4a0c930a154bee0271654282a1a6f195b368868a1366b
  - type: url
    url: 'https://agents.md/'
    hash: sha256:5ec43d6577c80fd2ba9a6b8db4aa810296c14fbd3d8a190442a89a81f486cf24
  - type: url
    url: 'https://arxiv.org/pdf/2601.20404'
    hash: sha256:a73a7d48c7792ddb34e456bd8a12088273326af22933553ee5bf51dfcf545cc2
  - type: url
    url: 'https://nyosegawa.com/en/posts/coding-agent-workflow-2026/'
    hash: sha256:bb7d36388cc5d0dc91fc90185585f6fff68833b1b198e732c6e2d6d41a285f45
  - type: url
    url: 'https://www.jeffmixon.com/post/dotagents-standard-agent-skill/'
    hash: sha256:b41f531a8b968768046d0a7c12e5e9658ea9dd26d4b4f3ece81e2e7340854718
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A repository-level Markdown context file for agentic AI coding tools, published as an open, tool-agnostic format and now stewarded by the Agentic AI Foundation. Empirical work has identified it as the emerging interoperable standard among competing tool-specific context file formats."
---

AGENTS.md is a repository-level Markdown [[DefinedTerm/context-files]] read by agentic AI coding tools. Its official site describes it as "a simple, open format for guiding coding agents" and states it is used by over 60,000 open-source projects, a figure the site sources to a GitHub code search. Per [[ScholarlyArticle/configuring-agentic-ai-coding-tools]], it serves as an open tool-agnostic convention increasingly supported across tools — in contrast to vendor-specific alternatives such as CLAUDE.md, GEMINI.md, and copilot-instructions.md.

## Usage

### The format's own description

The official site frames the file as "a README for agents": a dedicated, predictable place to provide the context and instructions that help AI coding agents work on a project. Its stated rationale for keeping this separate from README.md is that READMEs are for humans — quick starts, project descriptions, contribution guidelines — while AGENTS.md holds the extra, sometimes detailed context agents need, such as build steps, tests, and conventions that would clutter a README or are irrelevant to human contributors. The site gives three reasons for the separation: a clear, predictable place for agent instructions; concise, human-focused READMEs; and precise agent-focused guidance that complements existing docs. The site also states the name and format were chosen so they could work for anyone, rather than introducing another proprietary file.

There are no required fields. The site states that AGENTS.md is just standard Markdown and that any headings may be used, since the agent simply parses the text provided. As popular sections to cover it suggests project overview, build and test commands, code style guidelines, testing instructions, and security considerations, and adds that anything one would tell a new teammate — commit message or pull request guidelines, security gotchas, large datasets, deployment steps — belongs there too. It advises treating the file as living documentation.

Two behavioural rules are stated. In a monorepo, another AGENTS.md may be placed inside each package: agents read the nearest file in the directory tree, so the closest one takes precedence and every subproject can ship tailored instructions; the site notes that at time of writing the main OpenAI repo has 88 AGENTS.md files. Where instructions conflict, the closest AGENTS.md to the edited file wins, and explicit user chat prompts override everything. On testing commands, the site states that if they are listed, the agent will attempt to execute relevant programmatic checks and fix failures before finishing the task.

For projects with an existing agent-instruction file, the site suggests renaming it and creating a symbolic link for backward compatibility (`mv AGENT.md AGENTS.md && ln -s AGENTS.md AGENT.md`). Two tools need explicit configuration to read the file: Aider via `read: AGENTS.md` in `.aider.conf.yml`, and Gemini CLI via `{ "context": { "fileName": "AGENTS.md" } }` in `.gemini/settings.json`.

### Origin and stewardship

Accounts of where the format came from differ by source, and are worth keeping distinct. The official site says AGENTS.md "emerged from collaborative efforts across the AI software development ecosystem, including OpenAI Codex, Amp, Jules from Google, Cursor, and Factory". [[ScholarlyArticle/configuring-agentic-ai-coding-tools]], writing about the format rather than publishing it, describes it as introduced by [[Organization/openai]]. The site states that the format is now stewarded by the [[Organization/agentic-ai-foundation]] under the Linux Foundation.

### Empirical adoption

That study identifies AGENTS.md as the emerging interoperable standard, on evidence from three directions. In file counts it is close behind CLAUDE.md — 1,572 files (32.3%) against 1,661 (34.2%) — and it appears in 1,069 of the 2,634 repositories that contain context files (40.6%), against CLAUDE.md's 1,195 (45.4%). In creation order, where both are present, CLAUDE.md typically appears first and AGENTS.md is added later. And in reference patterns it is the most-referenced context file by a wide margin, receiving 368 incoming references; the single strongest pattern observed was CLAUDE.md pointing to AGENTS.md, occurring 311 times.

The authors read this as bottom-up convergence driven by developer practice and compatibility needs rather than by vendor mandate, noting that repositories which began with copilot-instructions.md often later introduced CLAUDE.md or AGENTS.md even though Copilot already supported all major context file types. They suggest that native support for AGENTS.md — already provided by Cursor and Codex — may become a baseline expectation for tool vendors. As of the study's February 2026 snapshot, the authors note Claude Code did not yet support it, which they offer as one possible explanation for the creation-order pattern in which CLAUDE.md appears first and AGENTS.md is added later.

Their practitioner guidance follows from this: developers who rely on multiple tools should consider maintaining an AGENTS.md file as a shared configuration baseline, with tool-specific files acting as adapters that reference a shared core file. The same study cautions that layering multiple context files in one repository raises the risk of redundant or conflicting instructions across artifacts.

Practitioner material frames the file in the same interoperability terms the study derives statistically. [[Person/arun-gupta]]'s [[PresentationDigitalDocument/spec-driven-development-using-coding-agents]] also describes it as a "README for agents" — a clear, predictable place for AI instructions — and lists its value as context that persists so the agent remembers the project across sessions, one file that works with many agents, zero onboarding time so new sessions start productive immediately, and built-in guardrails that prevent common mistakes before they happen. In the spec-driven workflow that deck proposes, `AGENTS.md` carries what the agent should *know*, distinct from skills, which carry what it should *do*, and the implementation plan, which carries what is being built.

### As OpenAI describes it

OpenAI's own description, in [[BlogPosting/introducing-codex]], is briefer than the empirical accounts above and worth keeping separate from them. AGENTS.md files are "text files, akin to README.md", placed within a repository, in which the developer can tell the agent how to navigate the codebase, which commands to run for testing, and how best to adhere to the project's standard practices. OpenAI frames the dependency by analogy: "Like human developers, Codex agents perform best when provided with configured dev environments, reliable testing setups, and clear documentation" — while claiming that its `codex-1` model performs strongly on coding evaluations and internal benchmarks even without AGENTS.md files or custom scaffolding, so the file is presented as an aid rather than a requirement.

The same post shows the file reaching into model behaviour rather than just tooling: OpenAI published the `codex-1` system message and gives, as its example of why that transparency is useful, that the system message encourages the agent to run all tests mentioned in the AGENTS.md file — something a user short on time can explicitly ask it to skip.

### Measured effect on agent efficiency

[[ScholarlyArticle/on-the-impact-of-agents-md-files]] is the first controlled measurement of what the file costs rather than of how widely it is adopted. Its design replays 124 real merged pull requests from 10 repositories at their pre-merge state, running an agent twice per task — once with the repository's own root `AGENTS.md` as it existed at that commit, and once with that single file deleted — so that repository, task, codebase state, and agent configuration are all held fixed.

With the file present, median wall-clock time to completion falls 28.64% (98.57s to 70.34s) and median output tokens fall 16.58% (2,925 to 2,440); both differences are reported as statistically significant. The two effects have different shapes, which the authors read separately: output-token savings concentrate in a small number of very high-cost runs, since the mean improves much more than the median, while the wall-clock improvement is uniform enough to indicate "a general shift toward faster task completion." Input and cached-input tokens barely move, and their medians go slightly the other way.

The authors' own hypothesis for the mechanism is that the file "describes repository structure and conventions upfront, reducing the need for agents to infer project organization through exploratory navigation," which they flag as speculation pending trace analysis.

The study measures efficiency only. It states explicitly that evaluating semantic correctness or functional equivalence to the merged pull request was out of scope, substituting a manual sanity check on 50 sampled tasks to confirm the agent produced non-trivial changes rather than aborted runs. So the finding is that a root instruction file makes the agent cheaper and faster on small, real tasks — not that it makes the work better. Set against the agentfiles study summarised in [[DefinedTerm/context-files]], which reports agents spending *more* reasoning tokens on context-file instructions without improving resolution rates, the two do not directly contradict: they measure different quantities on different task distributions, and neither measures cost and correctness together.

### Sizing it: a table of contents, not an encyclopedia

[[BlogPosting/survey-of-development-workflows-in-the-coding-agent-era]] collects the converged sizing guidance. It relays OpenAI's framing that these files should be treated as a table of contents rather than an encyclopedia, with a target of 60-150 lines; HumanLayer's tighter recommendation of 60 lines or fewer; and a Vercel report of compressing 40KB to 8KB while maintaining a 100% pass rate. The recommended pattern in all three cases is [[DefinedTerm/progressive-disclosure]] — file pointers in the top-level file, details split into subfolder context files, skills, or external docs.

The same post relays a result that cuts against loading everything on demand. In a Vercel case study on Next.js 16, an 8KB `AGENTS.md` document index reached a 100% pass rate, 47 points above skills-based retrieval at 53%, with the stated explanation that passive context — always available — beat on-demand retrieval. That is one team's evaluation on one codebase rather than a general finding.

It also lays out how the files divide labour in practice: `AGENTS.md` as the tool-agnostic universal brief for what to do, `CLAUDE.md` for Claude Code-specific operational instructions, and an optional `SOUL.md` for agent personality. And it records the governance milestone — the format, released by OpenAI in August 2025, was transferred to the Linux Foundation's [[Organization/agentic-ai-foundation]] in December 2025 — along with adoption figures of 60,000-plus open-source projects and support across Claude Code, Codex, Cursor, Copilot, Gemini CLI, Windsurf and Aider.

### The router pattern

Where the sizing guidance above says how long the file should be, [[DefinedTerm/dotagents]] proposes what it should *contain*: nothing but conditional pointers. [[BlogPosting/dotagents-standard-agent-skill]] describes the file becoming a slim, always-read **router** whose job is to tell the agent where to look for deeper context, with the heavy material moved into a hidden `.agents/` directory organised by kind — rules, context, memory, personas, skills, specs and logs.

Its diagnosis of why these files bloat is worth recording separately from the fix, because it explains why length caps alone do not hold. Each addition earned its place the day it was written — a schema excerpt because the agent kept guessing a column name wrong, a paragraph on voice and tone after a derived document read badly, a hard-won CI scar so nobody re-learns it expensively — and "the failure mode is cumulative," ending with an agent reading a database schema while it edits CSS.

The mechanical requirement that post insists on is conditionality. A routing rule must name a trigger and carry an action verb, so that the agent knows both when the pointer applies and what to do with it; an unconditional "always read everything" router "just recreates the monolith one directory deeper."

## Related Terms

[[SoftwareApplication/cursor]] deprecated its earlier `.cursorrules` context file and now suggests using AGENTS.md instead; [[SoftwareApplication/codex-cli]] reads AGENTS.md alongside an AGENTS.override.md variant, and [[SoftwareApplication/codex]] is guided by it in the cloud as well. The official site additionally lists [[SoftwareApplication/jules]], [[SoftwareApplication/gemini-cli]], [[SoftwareApplication/github-copilot]]'s coding agent, and a broad set of other agents and editors as compatible with the format.
