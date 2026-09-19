---
title: "Practical Implementation Report on Introducing Spec-Driven Development Using AI Agents in Software Development PBL"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, spec-driven-development, software-engineering-education]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2608.30572'
    hash: sha256:c0eb1ba213f36e53531516aecba8c4127b4017c1605a1fac8aba65de8f96ce7d
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A 2026 implementation report on introducing spec-driven development with AI agents into a third-year undergraduate team-development course, analysing per-phase AI usage, added lines of code across four academic years, and instructor-assessed code comprehension."
  author: ["Hidetake Tanaka", "Hiroshi Igaki", "Kazumasa Shimari", "Kiyoshi Honda", "Naoki Fukuyasu"]
  datePublished: "2026"
  keywords: ["Software Engineering Education", "Project-based Learning", "AI Agents", "Large Language Models"]
---

This implementation report describes introducing [[DefinedTerm/spec-driven-development]] into a Software Development Project-Based Learning course — the "Information System Development Exercise" elective for third-year Department of Information Systems students at Osaka Institute of Technology, a 14-lecture course in which teams of three to four build a database-backed web application in Java and Spring Boot. The authors adapted the spec-driven workflow into four phases — investigation, planning, implementation and review — in which AI agents generate artifacts at each step. Their stated adaptation is to redefine the requirements-analysis and design phases of the existing workflow as a single investigation phase, on the reasoning that this generalizes it to cover feature additions and debugging rather than only new requirements, and to add an explicit review phase in which both the agent and the student confirm the implementation matches the specification and follows coding conventions.

The course infrastructure is as much the subject of the report as the workflow. Each team received a template project directory for Visual Studio Code containing a `copilot-instructions.md` file carrying the workflow and project-specific rules as custom instructions, a `docs/` directory holding `specs.md`, `tasks.md` and a `reports/` subtree with `investigate/`, `review/` and `done/` directories for the corresponding reports, and a `NewSpringBootProject/` directory in which the team creates its own Spring Boot project. Instructors delivered a lecture on GitHub Copilot's agent mode, vibe coding and spec-driven development, then performed one full cycle of the workflow live in front of the students. The study analyses team activity from November 2025 to January 2026 along three axes: weekly self-reported AI usage per phase on a five-point scale, lines of code added per student per lecture mined from the team Git repositories, and code comprehension assessed by instructors in one-on-one interviews on a four-level scale.

## Key Points

- Reports that AI usage patterns varied substantially across phases and teams: in the implementation and debugging phases — the ones tied to producing and understanding source code — every team used AI to some degree, while in the investigation and planning phases usage differed sharply between teams, and in the review phase no team used AI much.
- Finds implementation throughput rose over the four academic years studied: Steel-Dwass tests on added lines of code found statistically significant year differences in seven of eight lectures, with earlier years (2022, 2023) consistently lower than later ones (2024, 2025) and no instance of a later year being significantly lower — a pattern the authors describe as corresponding temporally with the proliferation of LLM technologies.
- Reports that students at AI usage level 0 on the 0–4 scale — those who implemented code without using AI — maintained consistently high code comprehension across all three periods the comprehension analysis covers, and that students at level 3 implemented code with very little comprehension, especially during the middle period (lectures 9–10).
- States nonetheless that across the student body as a whole no clear statistical trend was confirmed between AI usage level and code comprehension, attributing this to the limited sample size, high individual variability, and the possible effect of the instructors' own timely interventions.
- Describes one observed cycle offered as an example of that intervention effect: in the lecture where AI usage peaked, comprehension scores dropped, and following instructor support comprehension recovered measurably the following week.
- Recommends three approaches for instructors: a foundation-first approach, in which the first five of fourteen sessions cover web-application and team-collaboration fundamentals before AI tools are used extensively; continuous monitoring with timely intervention, to detect comprehension drops early; and accountability for AI-generated code, where students are expected to explain the logic behind code they did not write by hand.
- Argues that spec-driven development is more suitable than vibe coding for a course aimed at cultivating application development skills, because students must understand the specifications and take responsibility for the agent's outputs — documentation and source code alike — which the authors say makes it the more demanding of the two.
- Reports that the standardized project templates appeared to help students start development with AI agents smoothly, and suggests they serve two audiences at once: concrete examples of how to structure instructions for less experienced students, and a foundation for customization for those already familiar with the tools.

## Notes

The authors set out three limits on the findings themselves. There was no concurrent control group abstaining from AI agents; the comparison is against historical cohorts from 2022 to 2024, so year-to-year variation in student skill, differences in cohort size — the course ran with 38 students in 2022, 28 in 2023, 25 in 2024 and 14 in 2025 — and changes in the educational environment cannot be ruled out as confounders. Added lines of code is acknowledged as a partial proxy for development efficiency, capturing neither design quality, refactoring nor the removal of redundant code, and the comprehension scores rest on instructors' subjective assessment rather than objective tests, which the authors defend as the way to reach depth of understanding through dialogue while conceding the loss of rigor. The study covers a single course using Java and Spring Boot with four teams, so the authors present it as informative for similar project-based courses rather than generalizable.

The report closes by naming three directions for future work: developing effective methods to assess and improve students' understanding of AI-generated code, investigating workflows that balance AI assistance against learning outcomes, and longitudinal study of how early exposure to AI agents affects long-term software engineering skills.
