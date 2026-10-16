---
title: "ソフトウェア開発PBLへのAIエージェントを活用した仕様駆動開発の導入実践報告"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, spec-driven-development, software-engineering-education]
aliases: ["Implementation Report on Introducing Spec-Driven Development with AI Agents into Software Development PBL"]
sources:
  - type: url
    url: 'https://www.jstage.jst.go.jp/article/repit/2026/0/2026_90/_pdf/-char/en'
    hash: sha256:9ab8cfe40222ed8eac41d0ae082d11418fdd4a9d90555882dc21dc43c0c43802
review_status: pending
generated_at: "2026-10-16"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.10.0"

properties:
  description: "A practice report, published in the proceedings of the 12th Practical IT Education Symposium (rePiT2026), on introducing spec-driven development with AI agents into a third-year undergraduate software development PBL course, analysing students' self-reported AI use, lines of code added and instructor-assessed code comprehension."
  author: ["Hiroshi Igaki", "Kiyoshi Honda", "Naoki Fukuyasu"]
  datePublished: "2026"
---

This practice report, by three authors from the Faculty of Information Science and Technology at
Osaka Institute of Technology, describes introducing [[DefinedTerm/spec-driven-development]] into a
software development project-based learning (PBL) course for third-year undergraduates. The course is
a 14-week elective in which teams of three to four students build a database-backed web application
with the Spring Boot framework, sharing code on GitHub and following GitHub Flow; the first five
sessions are a framework tutorial and the PBL runs from the sixth session onward. The authors present
spec-driven development — an approach in which an AI agent generates code against structured
specification documents rather than ambiguous natural-language instructions — as better suited to such
a course than [[DefinedTerm/vibe-coding]], because students have to understand the specifications and
take responsibility for what the agent produces.

The workflow they defined has four phases — investigation, planning, implementation and review — in
each of which the agent, GitHub Copilot, generates documents or code. Compared with the
requirements-analysis, design and implementation-planning sequence of the existing workflow they draw
on, they replace requirements analysis and design with a single investigation phase, so that the
workflow covers feature additions and debugging as well as new requirements, and add an explicit
review phase in which the agent and the students check that the implementation matches the
specification and follows the coding conventions. Each team received a template project whose
`copilot-instructions.md` holds the workflow and project-specific rules as custom instructions, with
`specs.md`, `tasks.md` and directories for investigation, review and completion reports; instructors
gave a lecture on vibe coding and spec-driven development and then ran one full cycle of the workflow
in front of the students.

To follow the students, the weekly progress reports gained items on how each student had used the
agent, a team reflection on that use, and an opportunity for each student to explain the code they
had committed to an instructor. The analysis, centred on 11 November to 15 December 2025 and the
course's 2025 cohort of 14 students in four teams, combines three measures: per-session
self-assessments of how effectively the agent was used in each kind of work on a 0–4 scale, lines of
code added per student per session mined from the teams' repositories and compared with the 2022–2024
cohorts, and code comprehension rated by instructors from 0 to 3.

## Key Points

- In a survey of 248 students in a second-year Java programming course at the same university, 26
  reported not using generative AI at all, so roughly 90% had used it in some form — but mostly for
  code generation, code understanding and bug fixing, with almost no use for wider development work
  such as requirements analysis or implementation planning.
- Students' self-reported use of the agent rose as the course progressed, particularly for
  implementation, debugging, planning and code explanation, and many already used AI for debugging
  before spec-driven development was introduced.
- Use varied considerably between teams: every team used the agent for debugging, while for the
  other phases the gap between teams that used it and teams that did not was large, and some teams
  did not follow the workflow as taught.
- Many artifacts the workflow calls for were never committed, and `specs.md` — which the authors
  describe as the key document linking implementation to specification — often went unupdated, so
  from the tenth session a check of its correspondence with the implementation was added to the
  progress report.
- The team that used AI least showed the highest code comprehension, while comprehension tended to
  fall in the three teams that used AI more, especially as more complex features were implemented;
  the authors conclude that AI use is likely to impair students' code comprehension and that some
  instructor feedback, such as comprehension assessment, is important.
- Lines of code added per session increased year on year from 2022, with large increases between 2022
  and 2023 and between 2023 and 2024 but no large difference yet between 2024 and 2025; the authors
  read this as generative AI having affected output while AI agents had, so far, contributed little
  further.
- Students tended to judge for themselves when the agent was needed and to proceed flexibly rather
  than strictly following the spec-driven workflow.
- The authors conclude that appropriate instructor guidance and follow-up — template projects,
  demonstrations, reflection on AI use, and regular checks that students understand their code — are
  essential when AI agents are introduced.

## Notes

The 2025 results cover the course only up to its tenth session, the point at which the report was
written, and rest on four teams. The comprehension scores are instructors' own judgments, and the
lines-of-code comparison is made against earlier cohorts of different sizes — 38 students in 2022, 28
in 2023, 25 in 2024 and 14 in 2025. As future work the authors name how to combine support for
learning to use AI agents with the guidance on code comprehension that students need, in a course
that respects students' autonomy.
