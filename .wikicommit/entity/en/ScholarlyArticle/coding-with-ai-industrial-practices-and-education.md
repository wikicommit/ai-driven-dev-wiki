---
title: "Coding with AI: From a Reflection on Industrial Practices to Future Computer Science and Software Engineering Education"
type: "schema:ScholarlyArticle"
lang: en
tags: [ai-assisted-programming, agentic-coding, vibe-coding, empirical-study, verification]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.23982'
    hash: sha256:a806ccf598e23dfb4d7bb1b2cb36744d9fd70c0a757249c93fa572bfb2c59229
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A qualitative analysis of 57 curated YouTube videos published between late 2024 and 2025, capturing industrial practitioners' accounts of LLM coding tools. It reports development bottlenecks shifting toward code review, testing, and security assessment, and argues for curricular shifts in response."
  author:
    - "Hung-Fu Chang"
    - "Mohammad Shokrolah Shirazi"
    - "Lizhou Cao"
    - "Supannika Koolmanojwong Mobasser"
  datePublished: "2025-12-30"
---

"Coding with AI" is a paper by four authors at the University of Indianapolis, Marian University, the University of Maryland Eastern Shore, and the Boehm Center for Systems and Software Engineering, posted to arXiv on 30 December 2025.

Its stated gap is one of vantage point: "prior research has primarily examined AI-based coding at the individual level or in educational settings, leaving industrial practitioners' perspectives underexplored." Its method addresses that with an unusual source — a qualitative analysis of 57 curated YouTube videos published between late 2024 and 2025, "capturing reflections and experiences shared by practitioners," selected through a filtering and quality-assessment process and then coded into themes.

Three research questions organise it: what types of AI usage exist in programming and how they differ from traditional software development; what concerns and risks AI tool adoption introduces; and how AI tools reshape workflows and what new skills they demand.

## Key Contributions

- **A spectrum, not a binary.** Practitioners in these accounts describe three distinguishable approaches — [[DefinedTerm/vibe-coding]], AI-assisted coding, and [[DefinedTerm/agentic-coding]] — which the paper characterises as differing "in levels of AI autonomy and human involvement." That this distinction emerges from practitioner talk rather than from a taxonomy imposed by the researchers is part of the finding.
- **The bottleneck moves rather than disappears.** Across all three approaches, "code generation is significantly accelerated, while development bottlenecks shift toward code review, testing, security assessment, and system-level reasoning." The consequence the paper draws is a change in which skills matter: "skills related to reading, evaluating, and validating code become increasingly critical."
- **A consistent list of concerns.** The practitioner accounts report worries about code quality, maintainability, traceability, and security vulnerabilities in AI-generated artifacts, alongside ethical issues.
- **Lower barriers and a skills worry, held together.** The paper reports notable productivity gains and lowered barriers to entry, and in the same breath that practitioners raise "concerns about skill erosion, reduced problem-solving practice, and diminished learning opportunities for beginners," together with insufficient preparation of entry-level engineers.
- **An argument for curricular change.** From those findings the paper argues for shifts in computer science and software engineering education toward problem-solving and architecture rather than syntax-level coding practice.

## Notes

The methodological choice is the thing to weigh when reading these results. Analysing 57 YouTube videos captures what practitioners say publicly about their own work, which is a different quantity from what they do — it is subject to selection by whoever chose to make a video, by whatever the platform surfaced, and by the incentives of speaking publicly about tooling. The paper is explicit that it is a qualitative analysis of curated sources rather than a survey or a measurement study, and its findings are best read as an inventory of the concerns circulating in practitioner discourse in that period.

Read that way, they line up closely with what better-instrumented sources find. The bottleneck shift toward review is the same phenomenon the survey evidence records under [[DefinedTerm/verification-bottleneck]], and the review-time asymmetry measured in [[ScholarlyArticle/security-in-the-age-of-ai-teammates]] gives it a quantitative form. The three-way spectrum matches the distinctions drawn independently on [[DefinedTerm/vibe-coding]] and [[DefinedTerm/agentic-coding]]. The skill-erosion concern is the one this paper carries further than most, because its educational framing forces the question of what happens to practitioners who never learned the syntax-level practice the tools have absorbed.
