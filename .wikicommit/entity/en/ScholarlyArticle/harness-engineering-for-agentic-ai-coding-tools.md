---
title: "Harness Engineering for Agentic AI Coding Tools: An Exploratory Study"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, context-engineering, software-engineering, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2602.14690'
    hash: sha256:09e9ad225a048f9efa9c17ecb63a1279c9685e21a0d73a0dd61a4970114bc3aa
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A cross-tool study that documents eight repository-level configuration mechanisms offered by five agentic AI coding tools and measures their adoption in 2,853 open-source GitHub repositories, finding that context files dominate while Skills and Subagents remain rare."
  author: ["Matthias Galster", "Seyedmoein Mohsenimofidi", "Jai Lal Lulla", "Muhammad Auwal Abubakar", "Christoph Treude", "Sebastian Baltes"]
  abstract: "The paper presents a systematic analysis of configuration mechanisms for agentic AI coding tools, covering Claude Code, GitHub Copilot, Cursor, Gemini and Codex. It identifies eight mechanisms spanning static context to executable and external integrations and, in an empirical study of 2,853 GitHub repositories, examines whether and how they are adopted, with a detailed analysis of Context Files, Skills and Subagents."
  keywords: ["harness engineering", "context engineering", "configuration", "AI agents", "AGENTS.md"]
---

This paper asks which configuration mechanisms agentic AI coding tools offer, and how developers
actually use them in open-source repositories. It frames the question through a layered vocabulary:
*context* is the complete input to a single model call; the *agent harness* is the software around
the model that drives the agent loop, assembles that context for each call, exposes tool schemas and
manages turn-by-turn state; [[DefinedTerm/context-engineering]] is the practice of designing the
context the harness assembles at runtime; and customizing the harness itself for a project — not only
the context — is what the authors call [[DefinedTerm/harness-engineering]]. A *configuration
mechanism* is any means by which developers tailor tool and agent behaviour to a project or workflow,
and a *configuration artifact* is a concrete, repository-versioned instance of one, such as a
`CLAUDE.md` file or a skill directory.

The authors first reviewed the documentation of [[SoftwareApplication/claude-code]],
[[SoftwareApplication/github-copilot]], [[SoftwareApplication/cursor]] (CLI),
[[SoftwareApplication/gemini-cli]] and the [[SoftwareApplication/openai-codex]] CLI, and derived
detection heuristics from file and directory names. They then sampled engineered open-source projects
on GitHub — non-fork, licensed, multi-contributor repositories created before 2024 and active since
June 2025, with an LLM classifying README files to keep only projects showing clear software
engineering practices — and found 2,853 repositories that use one or more of these tools. Beyond
overall adoption, they analysed three mechanisms in detail: context files and Skills, because every
tool supports them, and Subagents, because they share the Skills format.

Their headline reading is that developers widely adopt static context mechanisms but rarely the
executable and external ones, so that "harness engineering in open source today is therefore mostly
context engineering". They present their results as an empirical baseline and a point-in-time
snapshot (February 2026) of conventions that are still consolidating.

## Key Points

- The paper documents eight repository-level configuration mechanisms: Context Files, Skills,
  Subagents, Commands, Rules, Settings, Hooks and MCP servers. Context Files and Skills are supported
  by all five tools studied, and no single tool implements all eight.
- Context files were the most frequently adopted mechanism, used by 61.5% to 100% of repositories
  across the tools; no other mechanism exceeded 20% adoption for Claude Code, Copilot, Cursor or
  Gemini, except that 72.8% of Cursor repositories adopt Rules and 62.3% of Gemini repositories use
  Settings. Codex (4 repositories) was too small to characterize.
- 70.6% of the repositories configure a single tool, and a further 493 (17.3%) use
  [[DefinedTerm/agents-md]] without any tool-specific configuration artifact.
- Claude Code repositories use the broadest range of mechanisms, Cursor projects emphasize Rules and
  Commands, and Copilot repositories rarely extend beyond context files.
- Of 4,768 context files found in 2,586 repositories (90.6% of the sample), `CLAUDE.md` was the most
  common (34.4%), followed by `AGENTS.md` (31.6%) and `copilot-instructions.md` (29.2%).
- In repositories with more than one context file type, `CLAUDE.md` was typically created first and
  `AGENTS.md` added later; `CLAUDE.md` most often points to `AGENTS.md` (301 cases), and `AGENTS.md`
  receives 353 incoming references, far more than any other file type. The authors read this as
  bottom-up convergence on `AGENTS.md` as a tool-agnostic standard, driven by developer practice
  rather than vendor mandate.
- The authors note that Claude Code, despite being the most popular tool in the sample, did not
  support `AGENTS.md` natively at the time of the study, which they describe as a gap between
  developer practice and tool capability.
- The study found 601 [[DefinedTerm/agent-skills]] in 158 repositories (median 2 per repository);
  85.5% include no additional resources, so Skills function primarily as structured text rather than
  executable scripts, and only 4.8% exceed the specification's recommended 500 lines.
- It found 450 Subagents across 131 repositories (median 2 per repository), and no repository using
  the persistent memory feature available for Claude Code's Subagents.

## Notes

The authors' practical recommendations follow from these findings: `AGENTS.md` is the simplest entry
point for configuring agentic tools; developers who use several tools should maintain it as the
shared core configuration, possibly structuring multiple context files hierarchically with
tool-specific files acting as adapters that reference it; Skills offer a way to bundle scripts and
structured resources for recurring workflows, though most do not; and tool-specific mechanisms such
as Rules or Commands tie workflows to one tool. They also flag that layering several context files in
one repository risks redundant or conflicting instructions, and call for longitudinal and controlled
studies of whether richer configuration measurably improves agent outcomes over context files alone.

Among the limitations they state: the heuristics detect the presence of configuration artifacts
rather than active tool use (a scan of commit histories found AI-authored commits in 72.1% of
repositories with at least one configuration artifact, which they treat as a lower bound); for
Copilot, Cursor and Gemini some detected files also apply to non-agentic modes; the "engineered
project" classification relied on a single labelling run of one LLM; and the sample covers only
open-source GitHub repositories.

The paper is an extended version of "Configuring Agentic AI Coding Tools: An Exploratory Study",
published at AIware '26 (Montreal, July 6–7, 2026). The authors are affiliated with the University of
Bamberg, Heidelberg University and Singapore Management University.
