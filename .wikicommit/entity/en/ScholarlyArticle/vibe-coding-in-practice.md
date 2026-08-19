---
title: "Vibe Coding in Practice: Motivations, Challenges, and a Future Outlook – a Grey Literature Review"
type: "schema:ScholarlyArticle"
lang: en
tags: [vibe-coding, ai-assisted-programming]
sources:
  - type: url
    url: 'https://arxiv.org/html/2510.00328v1'
    hash: sha256:b2c0a6654af54f57a7e60e8031d5b71ee36c0c875804c8a0ac5cb42ba4d8026b
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A systematic grey literature review coding firsthand practitioner accounts of vibe coding into motivations, experiences, perceptions of code quality and QA practices. Its central finding is a speed–quality trade-off paradox: Speed & Efficiency accounts for 62% of the 140 coded motivation units, \"Fast but Flawed\" for 68% of the 114 code-quality units, and Skipped QA for 36% of the 132 QA-practice units — one study's coding of self-selected practitioner accounts."
  datePublished: "2025-09-30"
  author: ["Ahmed Fawzy", "Amjed Tahir", "Kelly Blincoe"]
  keywords: ["vibe coding", "AI-assisted programming", "AI-generated code", "grey literature review", "quality assurance"]
---

This paper, by Ahmed Fawzy and Amjed Tahir of Massey University and Kelly Blincoe of the University of Auckland, is a systematic grey literature review of practitioner accounts of [[DefinedTerm/vibe-coding]]. Its stated gap is that despite widespread adoption, "no research has systematically investigated why users engage in vibe coding, what they experience while doing so, and how they approach quality assurance (QA) and perceive the quality of" the generated code; the authors describe their study as "the first empirical investigation of how users actually engage in vibe coding, especially outside formal development settings."

Its working definition is behavioural rather than definitional: "Vibe coding is the practice where users rely on AI tools through intuition and trial-and-error without necessarily understanding the underlying code." The method extracts **behavioral units** — single coded instances capturing something relevant to a research question — at the quote level rather than the article level, so several distinct behaviours in one article each become separate units. The search retrieved 154 grey literature sources such as blog posts, online articles and technical reports, of which 53 were excluded: 40 for falling below a quality threshold of ≥10/15 and 13 on the inclusion and exclusion criteria.

## Key Contributions

The four research questions each produced a coded distribution, which is the paper's most portable output.

- **Motivations (140 units).** Speed & Efficiency 62%, Accessibility & Empowerment 14%, Learning & Experimentation 11%, Creative Exploration 6%, Fast Prototyping 3%, Reducing Mental Effort 1%.
- **Experiences (132 units).** Instant Success & Flow 64%, Prompt Struggle & Iteration 13%, Code Breakdown or Abandonment 11%, Fun & Creative Satisfaction 8%, AI Hallucinations 2%, Confusion or Misunderstanding 2%.
- **Perceptions of code quality (114 units).** Fast but Flawed 68%, Fragile or Error-Prone 19%, Sloppy or Low Maintainability 4%, Prototype-Ready Only 4%, High Quality & Clean 3%, Misleading Confidence 1%.
- **QA practices (132 units).** Skipped QA 36%, Manual Testing or Edits 29%, Uncritical Trust 18%, Delegated QA to AI 10%, Reprompting Instead of Debugging 5%, Run-and-See Validation 2%, QA Breakdown or Confusion 1%.

Three named observations follow from those distributions.

**The speed–quality trade-off paradox.** Vibe coders knowingly accept flawed generated code in exchange for rapid progress, but the trade-off manifests differently by background: non- and novice developers concede that "it's not really coding" while remaining excited by what they can build, whereas experienced developers value speed but balance it with caution — the 29% who report making manual adjustments or adding tests. The authors' conclusion is that "while vibe coders are willing to tolerate imperfect code for speed, only experienced users have the skills to fix problems when they arise."

**The QA crisis in AI-assisted development.** The paper calls the systematic breakdown of traditional QA practices "the most observed concerning issue", with a majority of coded QA practices representing a departure from code verification. The factors it names are technical barriers — generated code being hard to debug because it can lack architectural structure and the contextual details developers rely on, such as comments, assumptions, or information about how the code integrates with the larger system — plus confusion when trying to understand generated code, and false confidence created by the "instant success" experience. Its warning is organizational rather than per-project: once teams get used to shipping fragile code without proper QA, the quality bar may drop across the organization, creating a culture where untested code is acceptable.

**A new class of vulnerable developers.** The 14% motivated by accessibility and empowerment include non-developers who build applications without prior coding skills, and the paper argues this democratization "often leaves them unprepared when problems arise", with sources illustrating people reaching dead ends at bugs they cannot diagnose. It names a **novice developer trap**, where failures lock beginners into reprompt–paste loops, accepting fragile behaviour when they cannot restore alignment between their intent and what the generated code actually does.

## Notes

The paper's recommendations are addressed to three audiences separately. For practitioners: use vibe coding to explore and prototype quickly, but "never promote to production without adding guardrails: tests, code review, and traceable decision records" — specifically why an AI change was accepted, which checks passed, accepted risks, and a short prompt/response ID log. For tool designers: incorporate lightweight verification, keep reminding users about QA, offer static and dynamic analysis as a real-time indicator of performance, security and missing tests, and address uncritical trust with step-by-step walkthroughs, visual diagrams or inline explanations. For organizations: match tasks to skill and provide scaffolds — guided debugging, safe templates, escalation paths — so newcomers learn to diagnose issues rather than outsource all QA.

The authors state the limits of the design plainly. The study rests on sources from practitioners "who chose to share their stories online", which introduces self-selection bias, mitigated by seeking diversity across source types and user roles but not eliminated; the findings "cannot be considered generalizable to all vibe coders" and should be read as "indicative of common patterns in reported experiences" rather than representative of the population. One external comparison is offered: the paper cites the Stack Overflow Developer Survey 2025 as reporting both high adoption of AI tools (84% use or plan to use them) and low trust in generated code (around 46% reporting distrust).

Two details of the extracted text are worth recording for anyone checking these figures. Several LaTeX macros did not expand in the version ingested here, so the paper's own totals for included sources and behavioral units appear as unresolved placeholders; the per-research-question counts above are the figures the Results section states directly. The paper is a preprint version (v1).
