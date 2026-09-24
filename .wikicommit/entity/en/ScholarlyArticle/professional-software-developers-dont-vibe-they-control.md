---
title: "Professional Software Developers Don't Vibe, They Control: AI Agent Use for Coding in 2025"
type: "schema:ScholarlyArticle"
lang: en
tags: [vibe-coding, coding-agents, human-oversight, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.14012'
    hash: sha256:3197fbddd31215618ab26a5273b706ca5432b3bd07709d27db0f059144250823
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A two-part study — 13 field observations and a qualitative survey of 99 developers — of how experienced software developers used AI coding agents in 2025, finding that they control agents through planning and supervision rather than vibe coding."
  author: ["Ruanqianqian (Lisa) Huang", "Avery Reyna", "Sorin Lerner", "Haijun Xia", "Brian Hempel"]
  keywords: ["[[DefinedTerm/agentic-coding]]", "[[DefinedTerm/vibe-coding]]", "experienced developers", "task suitability"]
---

A paper by Ruanqianqian (Lisa) Huang, Avery Reyna, Sorin Lerner, Haijun Xia and Brian Hempel (Cornell University, UC San Diego and an independent researcher) that asks how experienced developers — defined as having at least three years of professional development experience — actually create software with AI agents, where "agents" means AI tools integrated into an IDE or terminal that can manipulate code directly. Unlike earlier studies of [[DefinedTerm/vibe-coding]], the authors do not restrict the investigation to vibe coding, and they examine experienced developers only. Their research questions cover what these developers value when integrating agents, the strategies they use, which tasks agents suit, and how they feel about working with them.

The study has two parts, both run between August and October 2025. In the first, 13 developers with 3 to 25 years of professional experience worked for 45 minutes on a self-chosen task with their usual agentic setup while thinking aloud, followed by a 30-minute semi-structured interview. In the second, the authors emailed 4,141 GitHub users drawn from AI-related repositories, received 249 responses, and analysed 99 qualified respondents after discarding five responses they judged to be AI-generated; respondents averaged 12.8 years of professional experience. The authors analysed both parts with thematic analysis, followed by targeted analyses of the observed prompts and of the 189 tasks mentioned in survey responses.

The headline finding is in the title: experienced developers do not vibe code. They value agents as a productivity boost but retain their agency over software design and implementation, controlling agent behaviour through planning and supervision because they care about software quality.

## Key Points

- Developers valued agents for accelerating their work while also valuing software quality attributes; 67 of the 99 survey respondents named quality attributes such as correctness and readability as priorities when working with agents.
- In the survey, Claude Code (58 of 99), GitHub Copilot (53) and Cursor (51) were the most-used tools; in the observations, Cursor (6 of 13) and Claude Code (4 of 13) were the most used.
- All 13 observed developers controlled implementation at some level, and 11 of them controlled design by writing plans themselves, revising agent-drafted plans, or asking the agent to polish a human-written plan. Nine of the 13 — all working within their own domain of expertise — carefully reviewed every agentic change.
- Plans were executed in small chunks to keep control: two participants' plans exceeded 70 steps, yet neither ever had an agent execute more than six steps at once, and the median participant asked for 1.8 steps per prompt.
- Developers controlled agents through prompts with clear context and explicit instructions, through user rules, and through established software-engineering practice such as reading diffs, testing, decomposing tasks and version control; they cited their own domain expertise as critical to using agents effectively.
- Survey respondents found agents suitable for straightforward, repetitive and scaffolding work when prompted with well-defined plans — for example accelerating productivity (35 respondents saying suitable to 2 unsuitable), small or straightforward tasks (33:1), following well-defined plans (28:2), tedious or repetitive tasks (26:0), scaffolding (25:0), writing documentation (20:0) and writing tests (19:2).
- Agents were judged unsuitable as complexity rose: one-shotting code without modification or verification (5:23), integrating with existing or legacy code (3:17), complex tasks (3:16), business logic or tasks needing domain knowledge (2:15), and replacing human expertise or decision-making (0:12). No respondent said agents were suitable for completely autonomous operation.
- Using agents for high-level planning and architecture design was the most contested use (13 suitable to 23 unsuitable).
- Developers generally enjoyed working with agents — survey respondents rated their enjoyment 5.1 out of 6 on average compared with working without them — but as a source of collaboration with a human in the loop rather than as complete delegation.
- The authors give four reasons experienced developers avoid vibing: they value software-engineering principles that are hard to instil in agents; they work on production software with real stakeholders; predefined requirements in familiar codebases leave little room for exploratory coding; and failed agentic solutions in unfamiliar domains can take a long time to resolve.

## Notes

The authors list several threats to validity: the survey was deliberately biased toward people positive about AI, which suited the questions on strategies and task suitability but less so the question on sentiment; the observation sample is small; 12 of 13 observation participants and 97 of 99 survey respondents self-identified as male; recruiting through scraped public GitHub emails may bias toward developers active on AI/ML repositories; and each observation was a single 45-minute session, so longitudinal use and full development cycles were not observed. The task-suitability thresholds (a ratio of at least 2.5:1 to count as "maybe suitable") were chosen by the authors' judgment as part of a reflexive analysis.

They acknowledge that agentic tools have improved since the study and may have shifted task suitability, but expect the core findings — that production software quality requires human supervision and clear human–agent communication — to persist. They call for future work on better interfaces for planning and controlling agents, and on rigorously developed best practices, noting that the patterns they observed may not be optimal.

The paper positions its results alongside other empirical studies of vibe coding, including [[ScholarlyArticle/vibe-coding-programming-through-conversation-with-artificial-intelligence]] and [[ScholarlyArticle/building-software-by-rolling-the-dice]], which it reads as also showing that vibe coding still demands programming expertise.
