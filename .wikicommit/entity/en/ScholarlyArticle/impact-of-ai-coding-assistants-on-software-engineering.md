---
title: "The Impact of AI Coding Assistants on Software Engineering: A Longitudinal Study"
type: "schema:ScholarlyArticle"
lang: en
tags: [developer-experience, productivity, empirical-study, human-oversight]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.23135'
    hash: sha256:3e017ddd415719f2210ad1a5afb381f4f70a87438df16f7b32b5c7121db023a7
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A University of Auckland longitudinal mixed-methods study that surveyed professional software engineers twice, six months apart, on how AI coding assistants change their task focus, developer experience and productivity, proposing the concepts of supervisory engineering work and a productivity-experience paradox."
  author: ["Annie Vella", "Kelly Blincoe"]
  datePublished: "2026-05"
  abstract: "Two questionnaires administered six months apart yielded 158 eligible participants at the first time point, 101 at the second and a matched cohort of 95. Participants reported spending less time on most development tasks, with 82% reporting less time writing code, and a broader shift from creation to verification activities. The study proposes supervisory engineering work — the direction, evaluation and correction of AI output — as a new category of work, and identifies a productivity-experience paradox: 84% reported improved productivity at both time points, yet among matched participants the share reporting worsened developer experience in at least one dimension nearly doubled from 14% to 27%."
  keywords: ["AI impact", "software engineering", "supervisory engineering", "productivity-experience paradox"]
---

This study by Annie Vella and Kelly Blincoe of the University of Auckland examines how professional
software engineers perceive the effects of AI coding assistants on their work, prioritising lived
experience over tool performance. It argues that most prior evidence is cross-sectional,
short-term, benchmark-based or drawn from students, and that productivity and developer experience
have usually been studied in isolation, so it tracks the same professionals over time and treats
the two jointly.

The authors ran two online questionnaires six months apart — in October 2024 and April 2025 —
yielding 158 eligible participants at the first time point, 101 at the second and a matched
longitudinal cohort of 95, drawn from 28 countries with the largest share in New Zealand. The
design was convergent parallel mixed methods: Likert-scale items on task focus across six
development tasks, the three dimensions of the DevEx framework (feedback loops, cognitive load and
flow state) and perceived productivity were analysed with non-parametric tests, and open-ended
responses were analysed with reflexive thematic analysis.

## Key Points

- Most participants perceived spending less time on the development tasks measured; writing code
  showed the steepest decline, with 82% reporting less time on it by the second questionnaire.
  Reviewing code was the only task whose mean sat above neutral at both time points.
- Among matched participants, the balance between verification tasks (reviewing, testing,
  debugging) and creation tasks (designing, writing, refactoring) shifted significantly toward
  verification, although neither group changed significantly on its own; the authors call this the
  [[DefinedTerm/creation-to-verification-shift]].
- Because the measured increase in verification was modest, the authors propose that the freed
  effort flows into [[DefinedTerm/supervisory-engineering-work]] — directing AI, evaluating its
  output and correcting its errors — a category they argue traditional SDLC taxonomies do not
  capture.
- Perceived productivity was high and stable (84% reporting improvement at both time points, 77% of
  matched participants giving identical ratings), while the share reporting worsened developer
  experience in at least one dimension nearly doubled from 14% to 27%. Feedback loops improved
  significantly; cognitive load and flow state showed non-significant declines. The authors term
  this the [[DefinedTerm/productivity-experience-paradox]].
- Changes in developer experience did not correlate with changes in productivity, in contrast to
  moderate-to-strong cross-sectional correlations between the two at each time point.
- The tool landscape shifted during the study: 82% of matched participants changed their tool
  combinations, the mean number of tools per participant rose from 1.9 to 2.9, ChatGPT usage fell
  from 70% to 58% and [[SoftwareApplication/cursor]] usage rose from 16% to 29%.
- Maintainability was the only concern whose ranking changed significantly, rising from 3% to 19%
  of participants' primary concern; quality remained the dominant primary concern.

## Notes

The authors acknowledge several limitations. Forty percent of first-questionnaire participants did
not complete the second, and engineers who became disillusioned may have been less likely to
respond. Only engineers currently using AI coding assistants were sampled, so the 84% productivity
figure should be read as 84% of continuing users; 85% of the sample were men and predominantly
English-speaking. The measures are perception-based and subject to recall bias, and the findings
reflect tools as they existed in late 2024 and early 2025, which may not hold for newer, more
autonomous agentic tools. The first author is a practising software engineer, which the authors
manage as a potential source of interpretive bias. They disclose using
[[SoftwareApplication/claude-code]] to help develop R scripts for statistical analysis and to review
the text for clarity.
