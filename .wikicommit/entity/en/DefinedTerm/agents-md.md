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
review_status: pending
generated_at: "2026-08-20"
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

## Related Terms

[[SoftwareApplication/cursor]] deprecated its earlier `.cursorrules` context file and now suggests using AGENTS.md instead; [[SoftwareApplication/codex-cli]] reads AGENTS.md alongside an AGENTS.override.md variant, and [[SoftwareApplication/codex]] is guided by it in the cloud as well. The official site additionally lists [[SoftwareApplication/jules]], [[SoftwareApplication/gemini-cli]], [[SoftwareApplication/github-copilot]]'s coding agent, and a broad set of other agents and editors as compatible with the format.
