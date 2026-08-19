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
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A repository-level Markdown context file for agentic AI coding tools, introduced by OpenAI and serving as an open, tool-agnostic convention. Empirical work has identified it as the emerging interoperable standard among competing tool-specific context file formats."
---

AGENTS.md is a repository-level Markdown [[DefinedTerm/context-files]] read by agentic AI coding tools. It was introduced by OpenAI and, per [[ScholarlyArticle/configuring-agentic-ai-coding-tools]], now serves as an open tool-agnostic convention increasingly supported across tools — in contrast to vendor-specific alternatives such as CLAUDE.md, GEMINI.md, and copilot-instructions.md.

## Usage

That study identifies AGENTS.md as the emerging interoperable standard, on evidence from three directions. In file counts it is close behind CLAUDE.md — 1,572 files (32.3%) against 1,661 (34.2%) — and it appears in 1,069 of the 2,634 repositories that contain context files (40.6%), against CLAUDE.md's 1,195 (45.4%). In creation order, where both are present, CLAUDE.md typically appears first and AGENTS.md is added later. And in reference patterns it is the most-referenced context file by a wide margin, receiving 368 incoming references; the single strongest pattern observed was CLAUDE.md pointing to AGENTS.md, occurring 311 times.

The authors read this as bottom-up convergence driven by developer practice and compatibility needs rather than by vendor mandate, noting that repositories which began with copilot-instructions.md often later introduced CLAUDE.md or AGENTS.md even though Copilot already supported all major context file types. They suggest that native support for AGENTS.md — already provided by Cursor and Codex — may become a baseline expectation for tool vendors. As of the study's February 2026 snapshot, the authors note Claude Code did not yet support it, which they offer as one possible explanation for the creation-order pattern in which CLAUDE.md appears first and AGENTS.md is added later.

Their practitioner guidance follows from this: developers who rely on multiple tools should consider maintaining an AGENTS.md file as a shared configuration baseline, with tool-specific files acting as adapters that reference a shared core file. The same study cautions that layering multiple context files in one repository raises the risk of redundant or conflicting instructions across artifacts.

Practitioner material frames the file in the same interoperability terms the study derives statistically. [[Person/arun-gupta]]'s [[PresentationDigitalDocument/spec-driven-development-using-coding-agents]] describes it as a "README for agents" — a clear, predictable place for AI instructions — and lists its value as context that persists so the agent remembers the project across sessions, one file that works with many agents, zero onboarding time so new sessions start productive immediately, and built-in guardrails that prevent common mistakes before they happen. In the spec-driven workflow that deck proposes, `AGENTS.md` carries what the agent should *know*, distinct from skills, which carry what it should *do*, and the implementation plan, which carries what is being built.

### As OpenAI describes it

OpenAI's own description, in [[BlogPosting/introducing-codex]], is briefer than the empirical accounts above and worth keeping separate from them. AGENTS.md files are "text files, akin to README.md", placed within a repository, in which the developer can tell the agent how to navigate the codebase, which commands to run for testing, and how best to adhere to the project's standard practices. OpenAI frames the dependency by analogy: "Like human developers, Codex agents perform best when provided with configured dev environments, reliable testing setups, and clear documentation" — while claiming that its `codex-1` model performs strongly on coding evaluations and internal benchmarks even without AGENTS.md files or custom scaffolding, so the file is presented as an aid rather than a requirement.

The same post shows the file reaching into model behaviour rather than just tooling: OpenAI published the `codex-1` system message and gives, as its example of why that transparency is useful, that the system message encourages the agent to run all tests mentioned in the AGENTS.md file — something a user short on time can explicitly ask it to skip.

## Related Terms

[[SoftwareApplication/cursor]] deprecated its earlier `.cursorrules` context file and now suggests using AGENTS.md instead; [[SoftwareApplication/codex-cli]] reads AGENTS.md alongside an AGENTS.override.md variant, and [[SoftwareApplication/codex]] is guided by it in the cloud as well.
