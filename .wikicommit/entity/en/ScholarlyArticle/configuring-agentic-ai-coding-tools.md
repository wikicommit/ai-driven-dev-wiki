---
title: "Configuring Agentic AI Coding Tools: An Exploratory Study"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, ai-assisted-programming, configuration]
sources:
  - type: url
    url: 'https://arxiv.org/html/2602.14690v1'
    hash: sha256:a95102e253d7131ba8bf5f38f7f1e738784be17159af65fa612395d8ed4800b9
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An arXiv paper dated 16 February 2026 presenting a systematic analysis of the repository-level configuration mechanisms offered by five agentic AI coding tools, together with an empirical study of their adoption across 2,926 GitHub repositories."
  author:
    - "Matthias Galster"
    - "Seyedmoein Mohsenimofidi"
    - "Jai Lal Lulla"
    - "Muhammad Auwal Abubakar"
    - "Christoph Treude"
    - "Sebastian Baltes"
  datePublished: "2026-02-16"
  keywords:
    - "Software Engineering"
    - "Generative AI"
    - "AI Agents"
    - "Configuration"
---

An exploratory study of how developers configure agentic AI coding tools through versioned, repository-level artifacts. The authors systematically document eight configuration mechanisms across [[SoftwareApplication/claude-code]], [[SoftwareApplication/github-copilot]], [[SoftwareApplication/cursor]], [[SoftwareApplication/codex-cli]], and [[SoftwareApplication/gemini-cli]], then examine whether and how those mechanisms are adopted in 2,926 GitHub repositories.

The paper defines a *configuration mechanism* as a means by which developers tailor tool and agent behaviour to a project or workflow, and a *configuration artifact* as the tangible specification of that mechanism — the actual Markdown or JSON file. The authors present this as the first cross-tool, cross-agent mapping of these mechanisms and their adoption patterns; prior empirical work, they note, had focused on single artifact types in isolation, most often repository-level context files.

## Key Contributions

- **A catalogue of eight configuration mechanisms**, identified from the documentation of the five tools: [[DefinedTerm/context-files]], [[DefinedTerm/agent-skills]], [[DefinedTerm/subagents]], Commands, Rules, Settings, Hooks, and MCP servers. Some are available in all five tools; others are tool-specific.
- **An adoption analysis across 2,926 repositories.** Context Files dominate and are frequently the sole configuration mechanism present; Rules, Settings, Commands, Skills, and Subagents each appear in fewer than 20% of repositories. Claude Code repositories exhibit the broadest configuration footprint, while Cursor projects emphasise Rules and Commands and Copilot and Codex repositories rarely extend beyond Context Files.
- **A detailed look at three cross-tool mechanisms.** Among Context Files, [[DefinedTerm/agents-md]] emerges as an interoperable standard, with the strongest observed pattern being CLAUDE.md pointing to AGENTS.md. Skills and Subagents are shallowly adopted: the median repository defines two of either, and 83.3% of the 601 Skills found included no additional resources, with static documentation more common than executable scripts where resources were present.
- **Practitioner guidance** derived from those findings: Context Files, and AGENTS.md in particular, are the lowest-friction entry point; teams using multiple tools should consider AGENTS.md as a shared configuration baseline with tool-specific files acting as adapters that reference it; and executable Skills should be adopted deliberately, only where the expected benefits justify the additional setup effort.

## Notes

The study's sampling pipeline began from a SEART-based selection of non-fork GitHub repositories with at least two contributors and a licence, created before 1 January 2024 with commits since 1 June 2025, filtered by language and activity — yielding 37,249 repositories. After excluding unavailable repositories, those without a README, and 994 with non-English READMEs, a GPT-5.2-based classification pipeline labelled 32,564 of the remaining repositories as "engineered" software projects; file-path heuristics then identified 2,926 that use one or more of the five tools.

The authors state several limitations directly. Their heuristics detect the presence of configuration artifacts, not whether the corresponding tool is actively used, so artifact presence remains a proxy for adoption. For GitHub Copilot, Cursor, and Gemini, the detected files apply to both conversational and agentic modes, so agentic usage cannot be isolated. The repository classification used a single labelling run without inter-model agreement, and 2,204 "unsure" cases were excluded. The study covers only open-source GitHub repositories, and its findings are described as a point-in-time snapshot of February 2026 — early empirical signals rather than settled findings.
