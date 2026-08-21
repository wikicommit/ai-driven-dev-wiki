---
title: "Agent READMEs: An Empirical Study of Context Files for Agentic Coding"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, configuration, context-engineering, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2511.12884'
    hash: sha256:76efb50fd6bc599d4c645aaa06af94e83bc6b60e90aba276e96846dab7b04058
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A large-scale study of 2,303 agent context files from 1,925 repositories, finding that they behave as evolving configuration artifacts rather than static documentation, and that developers specify functional guidance far more often than security or performance."
  datePublished: "2025-08"
  abstract: "The first large-scale empirical study of 2,303 agent context files from 1,925 repositories, characterizing their structure, maintenance and content, and identifying a gap in which non-functional requirements such as security and performance are rarely specified."
  keywords: ["Agentic Coding", "Autonomous Programming", "Documents"]
---

"Agent READMEs: An Empirical Study of Context Files for Agentic Coding" is a study by Worawalan Chatlatanagulchai, Hao Li, Yutaro Kashiwa, Brittany Reid, Kundjanasith Thonglek, Pattara Leelaprute, Arnon Rungsawang, Bundit Manaskasemsak, Bram Adams, Ahmed E. Hassan and Hajimu Iida, spanning Kasetsart University, the Nara Institute of Science and Technology, and Queen's University. It describes itself as the first large-scale empirical study of agent context files, analysing 2,303 files from 1,925 repositories to characterize their structure, maintenance and content. Its stated motivation is a practical one: the significant lack of accessible documentation for creating these files, which the authors say has historically forced developers into inefficient trial-and-error when configuring their agents.

## Key Findings

**These are not static documents.** The paper's central characterization is that agent context files "are not static documentation but complex, difficult-to-read artifacts that evolve like configuration code through frequent, small additions". The maintenance evidence is that a majority of Claude Code context files — 67.0% — are modified across multiple commits, with the same pattern slightly less frequent for GitHub Copilot (59.8%) and OpenAI Codex (59.4%), and Claude Code files receiving significantly more commits than either. The authors describe maintenance as occurring in short, rapid bursts, driven by small incremental content additions, with content deletions negligible. Their summary is that unlike conventional software documentation, often characterized as "write-once", these files behave as evolving configuration artifacts.

**Length differs by tool, independent of task complexity.** GitHub Copilot files (median 535.0 words) and Claude Code files (median 485.0 words) are of similar length with no statistically significant difference between them, and both are substantially longer than OpenAI Codex files — a gap the authors report as independent of task complexity, and read as developers providing a much larger volume of natural language instruction to those two agents. On structure, the paper reports a consistently shallow hierarchy anchored by a single H1 heading with H2 and H3 subsections defining major topics, which it suggests likely helps developers parse and maintain the documents quickly. On readability it is blunt: the documents are complex, with many falling into a "difficult" category the authors compare to high-school-level material.

**Content skews functional.** A manual classification identified 16 distinct instruction categories — two of them, Maintenance and Debugging, new relative to the authors' earlier work. The most prevalent was Testing at 75.9%, covering procedures for automated tests, followed by Implementation Details at 70.8% covering development guidance such as code style, and Architecture at 68.1% describing high-level system design. Roughly half the files contain a system overview, and 24.1% carry an AI Integration label in which developers explicitly define the agent's role and responsibilities within the project — reviewer, for example.

**The gap is in non-functional requirements.** Performance appears in 14.5% of files, Security in 14.8%, and UI/UX in 8.7%. The authors state the implication directly: developers use context files to make agents functional but "provide few guardrails to ensure that agent-written code is secure or performant", so that agents are extensively guided on "how" to build code functionally "but not necessarily on 'how to build it well' concerning quality attributes."

## Context

The classification rests on human labelling rather than automation: inspectors with between 4 and 17 years of programming experience reached an 80.3% agreement rate, with a third inspector resolving all disagreements through negotiated consensus, producing 2,069 final label assignments. The paper separately reports that automatic classification of these files is feasible and promising, which it frames as a direction rather than a result the content findings depend on.

The percentages describe the proportion of files containing at least one instruction in a category, not the proportion of a file's content devoted to it, so the categories overlap heavily by design. The corpus is open-source repositories, and the tool-by-tool comparisons are between files written for Claude Code, GitHub Copilot and OpenAI Codex specifically.
