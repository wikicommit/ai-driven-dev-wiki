---
title: "Agent READMEs: An Empirical Study of Context Files for Agentic Coding"
type: "schema:ScholarlyArticle"
lang: en
tags: [agent-config, agentic-coding, mining-software-repositories]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2511.12884'
    hash: sha256:9998f7bc02e25b961e2b210ee4e55729d031aa12a534dd5f8215776506659355
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A large-scale empirical study of 2,303 agent context files, such as AGENTS.md and CLAUDE.md, drawn from 1,925 repositories. It characterizes how these files are structured, maintained and filled, and finds that they carry plenty of functional context but few non-functional requirements such as security or performance."
  author: ["Worawalan Chatlatanagulchai", "Hao Li", "Yutaro Kashiwa", "Brittany Reid", "Kundjanasith Thonglek", "Pattara Leelaprute", "Arnon Rungsawang", "Bundit Manaskasemsak", "Bram Adams", "Ahmed E. Hassan", "Hajimu Iida"]
  datePublished: "2025-11-17"
  abstract: "Agentic coding tools take natural-language goals, break them into tasks and write or execute code with minimal human intervention, guided by agent context files that give persistent, project-level instructions. The paper studies 2,303 such files from 1,925 repositories to characterize their structure, maintenance and content, and reports a gap between the functional context developers provide and the non-functional requirements they rarely specify."
---

This paper studies the files that give [[DefinedTerm/agentic-coding]] tools their persistent, project-level instructions: agent context files, with [[DefinedTerm/agents-md]] and [[DefinedTerm/claude-md]] as its named examples. It describes itself as the first large-scale empirical study of them, covering 2,303 context files from 1,925 repositories, and sets out to characterize three things about them: their structure, how they are maintained, and what they contain.

Its content analysis classifies the instructions in these files into 16 instruction types. The headline finding is an imbalance between what developers write down and what they leave out: functional context such as how to run tests, implementation details and architecture appears in most files, while non-functional requirements such as security and performance appear in few. The authors read this as developers using context files to make agents functional while providing few guardrails to ensure that agent-written code is secure or performant, and conclude that better tools and practices are needed.

The paper was first submitted to arXiv on 17 November 2025 (arXiv:2511.12884) and revised on 9 August 2026; it is listed under Software Engineering (cs.SE).

## Key Points

- The study covers 2,303 agent context files from 1,925 repositories, which the authors present as the first large-scale empirical study of such files.
- The paper finds that context files are not static documentation but complex, difficult-to-read artifacts.
- It reports that these files evolve like configuration code, through frequent, small additions.
- The content analysis distinguishes 16 instruction types.
- The most common kinds of content are functional: test procedures (75.9% of files), implementation details (70.8%) and architecture (68.1%).
- Non-functional requirements are rarely specified: security appears in 14.8% of files and performance in 14.5%.
- The authors conclude that developers use context files to make agents functional while providing few guardrails to keep agent-written code secure or performant, and call for improved tools and practices.

