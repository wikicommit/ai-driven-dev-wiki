---
title: "How AI is transforming work at Anthropic"
type: "schema:Report"
lang: en
tags: [ai-adoption, developer-productivity, claude-code, future-of-work]
sources:
  - type: url
    url: 'https://www.anthropic.com/research/how-ai-is-transforming-work-at-anthropic'
    hash: sha256:768151bc1fd55f4171a86c1cf74c112f09821eebf20b00b6dcd176e957394536
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An Anthropic study of how AI is changing work for its own engineers and researchers, combining an August 2025 survey of 132 staff, 53 in-depth interviews and an analysis of 200,000 internal Claude Code transcripts."
  author: ["Saffron Huang", "Bryan Seethor", "Esin Durmus", "Kunal Handa", "Miles McCain", "Michael Stern", "Deep Ganguli"]
  publisher: "[[Organization/anthropic]]"
  datePublished: "2025-12-02"
  abstract: "Anthropic surveyed 132 of its engineers and researchers, interviewed 53 of them and analyzed internal Claude Code usage data to study how AI use is changing their work. It reports large self-reported productivity gains driven mainly by greater output volume, increasingly autonomous use of Claude Code on more complex tasks, and broader, more full-stack skill sets, alongside concerns about skill atrophy, supervising AI output, reduced collaboration and mentorship, and the long-term future of software engineering careers."
---

[[Organization/anthropic]] published this study in December 2025 as an inward-facing counterpart to its research on AI's economic impact across the labor market: instead of many occupations, it looks in detail at one group of early adopters — its own staff. In August 2025 it surveyed 132 engineers and researchers, conducted 53 in-depth qualitative interviews with survey respondents, and used a privacy-preserving analysis tool to study 200,000 internal [[SoftwareApplication/claude-code]] transcripts from February and August 2025. At the time the data was collected, Claude Sonnet 4 and Claude Opus 4 were the most capable models available.

The report acknowledges that studying AI's impact at a company building AI represents a privileged position — early access to cutting-edge tools, a relatively stable field — and says its findings likely do not generalize to other organizations yet. It publishes its survey questions and a limitations appendix: respondents were recruited through convenience and purposive sampling, interviewees were the first 53 people who responded, answers were not anonymous and so may carry social desirability bias, recalled figures from a year earlier may carry recency bias, and the transcript analysis can measure only relative, not absolute, changes in task distribution.

## Findings

- **Uses.** Debugging and code understanding were the most common uses: 55% of respondents used Claude for debugging daily, 42% for code understanding and 37% for implementing new features.
- **Usage and self-reported productivity.** Respondents reported using Claude in 28% of their daily work with a +20% productivity boost twelve months earlier, against 59% of their work and +50% now; 14% reported gains of more than 100%. The report notes that productivity is hard to measure and that a METR study found experienced developers overestimated AI's effect on their productivity, and reads its own figures as possibly reflecting employees' developing skill at choosing what to delegate.
- **Output rather than time.** Across almost all task categories, respondents reported a net decrease in time spent and a larger net increase in output volume; the report concludes that AI increases productivity at Anthropic primarily through greater output. Time savings clustered at both extremes, with some people spending more time on Claude-assisted tasks, for example debugging and cleaning up Claude's code.
- **New work.** Respondents estimated that 27% of their Claude-assisted work would not have been done otherwise — scaling projects, nice-to-have tools, documentation and testing, exploratory work — and 8.6% of Claude Code tasks were classified as fixing "papercuts," small quality-of-life improvements.
- **Limited full delegation.** More than half said they could "fully delegate" only 0–20% of their work to Claude, describing active supervision and validation especially for high-stakes work.
- **Delegation criteria.** Interviewees tended to delegate tasks that were outside their context but low in complexity, easily verifiable, well-defined or self-contained, low-stakes, repetitive or boring, and not faster to do than to prompt, while keeping high-level design and work requiring organizational context or "taste." Many described delegating progressively more complex work as trust grew, and called the boundary a moving target.
- **Skills.** Engineers reported becoming more "full-stack," working in areas such as front-end or databases they previously avoided, while some worried about [[DefinedTerm/skill-atrophy]] and losing the incidental learning that comes from solving problems by hand. The report names a [[DefinedTerm/paradox-of-supervision]]: using Claude well requires supervising it, and supervising it requires the coding skills that overuse may erode.
- **Craft, collaboration and careers.** Views divided on whether engineers miss hands-on coding. Claude had become the first stop for many questions that used to go to colleagues, and some senior engineers reported fewer questions from junior staff. Many described their role shifting toward managing and reviewing AI output, alongside widespread uncertainty about what their careers would look like in a few years.
- **Claude Code usage trends.** Between February and August 2025, average task complexity (on a 1–5 scale) rose from 3.2 to 3.8, the maximum number of consecutive tool calls per transcript rose by 116% (from 9.8 to 21.2), and average human turns per transcript fell by 33% (from 6.2 to 4.1). The share of transcripts implementing new features rose from 14.3% to 36.9% and of code design or planning from 1.0% to 9.9%.
- **Team differences.** Different teams used Claude Code to extend beyond their core expertise — for example the Security team largely for code understanding (48.9%), and non-technical employees largely for debugging (51.5%) and data science (12.7%) — which the report reads as everyone becoming more full-stack.

The report closes by describing follow-up steps inside Anthropic, including examining collaboration, professional development and best practices for AI-augmented work, and extending the research beyond engineers.
