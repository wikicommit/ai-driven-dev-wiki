---
title: "Desarrollo de software asistido por IA para profesionales con formaciones diversas"
type: "schema:ScholarlyArticle"
lang: en
tags: [ai-assisted-programming, software-engineering-education, github-copilot]
sources:
  - type: url
    url: 'https://revistas.unlp.edu.ar/JAIIO/article/download/19957/20195/95722'
    hash: sha256:7814321c9cdbe97832b83303a22a3f383abe37f211b944bce10796a1f3d358ef
review_status: pending
generated_at: "2026-10-16"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.10.0"

properties:
  description: "A Spanish-language paper from the Argentine Symposium on Computing Education (SAEI 2025, part of the 54th JAIIO) describing the design and implementation of a roughly 25-hour course on AI-assisted software development for professionals without formal software-engineering training, structured around SDLC phases with GitHub Copilot in Visual Studio Code used in every module."
  author: ["Matías Callara"]
  abstract: "This work presents aspects related to the design and implementation of a course on AI-assisted software development, aimed at professionals with diverse academic backgrounds. The main objective of the course is to familiarize students with relevant practices and tools in the industrial field that help them develop software effectively and efficiently, either collaboratively or individually."
  keywords: ["Desarrollo de software asistido por IA", "IA generativa", "prácticas de desarrollo de software", "código abierto"]
---

This paper, published in the proceedings of the Simposio Argentino de Educación en Informática (SAEI 2025) within
the 54th JAIIO, describes a course on [[DefinedTerm/ai-assisted-programming]] for professionals from fields outside
software engineering who have only basic programming exposure. The author motivates it by two trends: industries'
growing need for multidisciplinary teams, which creates demand for courses that teach effective development
practice to people without formal software-engineering training, and the rapid appearance of AI-based tools for
software development since large language models became widespread. It also gives an English title, "AI-Assisted
Software Development for Professionals with Diverse Backgrounds".

The course was first taught, in a preliminary version, in March 2024 as an elective in the Maestría en Análisis y
Gestión de Negocios at the Business School of Universidad Torcuato Di Tella. The paper describes the criteria behind
its design, its content, how it was delivered and evaluated, and closes with a discussion of the risks that easy
code generation poses for learners.

## Key Points

- The course runs to about 25 hours including lectures, practice and consultation, in five modules of five hours
  each, and is aimed at people who have done simple programming projects but come from outside software engineering.
- Its content is anchored to the phases of the software development life cycle (SDLC) rather than to specific
  tools, on the author's argument that those phases are more stable than the rapidly changing tools, and that a
  sound theoretical framework helps mitigate the risks of current AI use.
- Python was chosen as the language; non-AI tools such as Git, Virtualenv and Poetry, and Visual Studio Code with
  [[SoftwareApplication/github-copilot]] as the AI assistant, were selected using criteria including accessibility,
  stability, popularity, industry relevance and flexibility. Copilot's educational licence, favourable privacy
  conditions, wide adoption and frequent improvements are given as reasons for choosing it, and the paper leaves
  open replacing or complementing it with other AI tools in later editions.
- The five modules are version control (Git and GitHub, with Copilot suggesting commit messages, explaining
  commands and generating auxiliary files); Python packages, virtual environments and dependency management (Copilot
  helping with configuration files, installation scripts and environment errors); development and debugging in VS
  Code (Copilot suggesting fixes for common errors, helping write prompts and explaining code, alongside data-privacy
  considerations); testing and test-driven development with Pytest and Doctest (Copilot generating tests and, in
  TDD, proposing minimal implementations to iterate on the red-green-refactor cycle); and the SDLC, versioning and
  packaging with GitHub Actions and Python Semantic Release (Copilot drafting release notes and CI/CD configuration).
- The material is delivered as an interactive open-access book built with Jupyter Book, whose source is in a public
  GitHub repository so that the community can contribute and students can practise the Git and GitHub workflows the
  course teaches; a LinkedIn group extends the course beyond the classroom.
- Learning is assessed through end-of-module quizzes, practical assignments and an optional oral exam for extra
  points, and satisfaction through surveys after each module and at the end of the course.
- A survey after an initial version of the course reflected high satisfaction: participants valued the practical
  curriculum and the combination of industry-standard tools with AI assistants, and many said it increased their
  confidence to contribute to software projects. Difficulties installing and configuring the tools were a point of
  friction for some students, which led to tutorials for later editions. These results come from one course's
  student survey.

## Notes

The paper situates the course among MOOCs and university courses on AI in software development, noting that when it
was first taught most of those offerings did not yet exist or were not widely known. Its discussion argues that AI
assistance can speed up junior developers' learning through rapid prototyping and let senior developers focus on
design and architecture, but warns that in approaches such as [[DefinedTerm/vibe-coding]] code can be produced
without understanding the underlying principles and may look functional while lacking structure, error handling or
security considerations — which is why the author considers a firm grounding in software-development fundamentals and
critical thinking essential. The conclusion stresses that, while the SDLC-based structure is likely to last, the
rapid evolution of AI tools makes continual updating of the material necessary, motivating its open distribution.
