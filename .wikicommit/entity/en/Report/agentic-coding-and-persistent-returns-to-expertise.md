---
title: "Agentic coding and persistent returns to expertise"
type: "schema:Report"
lang: en
tags: [agentic-coding, ai-assisted-programming, empirical-study, metrics, human-ai-collaboration]
sources:
  - type: url
    url: 'https://www.anthropic.com/research/claude-code-expertise'
    hash: sha256:1c729c8632d41020cb46941b451021196758377dbc5b749dc33500941ab4506f
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An Anthropic economic research report of 16 June 2026 analysing roughly 400,000 interactive [[SoftwareApplication/claude-code]] sessions from about 235,000 people between October 2025 and April 2026. Its central finding is a stable division of labor — people make most planning decisions, the agent most execution decisions — and that domain expertise, not coding background, predicts whether a session succeeds."
  author:
    - "Zoe Hitzig"
    - "Maxim Massenkoff"
    - "Eva Lyubich"
    - "Shaoyi Zhang"
    - "Ryan Heller"
    - "Peter McCrory"
  publisher: "[[Organization/anthropic]]"
  datePublished: "2026-06-16"
---

"Agentic coding and persistent returns to expertise" is an economic research report published by [[Organization/anthropic]] on 16 June 2026. It rests on a privacy-preserving analysis of approximately 400,000 interactive [[SoftwareApplication/claude-code]] sessions from about 235,000 people between October 2025 and April 2026, covering usage through the CLI, Claude.ai, and the desktop app, and explicitly excluding non-interactive usage. It builds on two earlier Anthropic reports, on agent autonomy measures and on how Claude Code is changing work inside Anthropic.

The report's framing question is whether people without formal coding experience can successfully direct an agent through complex technical work, and what that implies for knowledge work more broadly. Its answer is a pair of claims held together: agentic coding is making a coding *background* less relevant to producing working software, while domain *expertise* — command of the problem being solved — remains what determines whether a session succeeds. Its own summary of this is that "coding agents are not substituting for domain expertise—the more understanding a worker brings to an agent, the more quality work the agent is able to do."

Every measure in the report is derived by classifiers reading session transcripts rather than from observed real-world outcomes, a limitation the authors state directly and return to at the end.

## Key Findings

- **A stable division of labor.** A decision-attribution classifier separates each session's decisions into planning (what to do, which approach, what counts as done) and execution (which files to change, what to write, which commands to run), then attributes each to the person or to Claude. On average people make about 70% of planning decisions and about 20% of execution decisions. The report's compact statement of this is that "people decide what to build, and the agent decides how to build it."
- **Expertise buys more work per instruction.** From each transcript a classifier rates the user's apparent expertise *at that task* on a five-point novice-to-expert scale, using three signals: how precisely directions are framed, what the user asks Claude to verify, and whether the user corrects Claude or the reverse. The report stresses this is task-specific rather than a job title — "a senior engineer asking their first Rust question is a beginner at Rust," while an accountant who has never used Python but specifies exactly which reconciliation rules a script must enforce is an expert at that task. In typical novice sessions each prompt sets off about five Claude actions and roughly 600 words of output; expert sessions set off about 12 actions carrying about 3,200 words. The trend holds within every kind of work and every task-value band, and survives a regression controlling for work mode, task value, month, occupation, and model family at +9% actions and +13% output per expertise level.
- **Expertise predicts success, with most of the gain at the bottom of the scale.** Novice-rated sessions reach *verified success* 15% of the time and at least partial success 77% of the time; sessions rated intermediate or above reach verified success 28–33% of the time and partial success 91–92%. Among sessions that hit trouble, verified success rises from 4% for novice-rated to 15% for expert-rated. The clearest behavioural difference is giving up: among sessions that hit trouble, 19% of novice-rated ones end *abandoned* — judged failed with zero lines of code written — against 5–7% for everyone else.
- **Occupation matters less than expertise.** People in software-related occupations reach verified success in about 30% of sessions overall against about 26% for other professions; among code-producing sessions the figures are 34% and 29%, and at least partial success is 89% against 88%. Every one of the ten largest occupation groups lands within seven percentage points of software engineers on code-producing sessions, and the gap has neither widened nor narrowed over the seven months even as both groups' success rates rose. Management occupations score highest on verified success, slightly above software engineering — which the authors suggest may reflect transferable management skill, but caution may also be a measurement artifact, since verification partly rests on explicit confirmation in the transcript and managers may be likelier to say when they got what they asked for.
- **The work moved away from debugging.** Sessions are classified into nine work modes — building, fixing, testing, orchestrating, operating, understanding, planning, analyzing, and communicating. Across the window, the share of sessions spent fixing broken code fell from 33% to 19%, operating software grew from 14% to 21%, and writing and data analysis roughly doubled from about 10% to 20%. Over the whole period about 56% of sessions were writing (25%), fixing (26%), or testing and orchestrating (5%), with operating at 17%, planning or exploring at 14%, and analysis or prose at 13%.
- **Task value rose.** Estimating each session's economic value by what the work would cost on a freelance marketplace, calibrated against a public dataset of real postings, the average session's estimated value rose 27% between October and April — about 43% for building, 34% for operating, and 32% for fixing. The report states these price estimates are coarse and are meant for comparing tasks over time rather than being read as dollar figures.
- **Session shape.** A typical session runs about four turns; each user prompt sets off a chain of around 10 Claude actions on average and sometimes over 100, with Claude writing an average of 2,400 words of output per turn. How much Claude does between check-ins tracks who decides: when the user makes over 80% of execution decisions Claude takes about eight actions per turn, and when Claude makes over 80% of planning decisions it takes about 16.

## Basis & Caveats

The evidence base is Anthropic's own telemetry and transcripts for its own product, analysed with its own classifiers — the report is transparent about this and about the validation it did and did not do. Session work-mode classifications were cross-checked against automatically recorded telemetry, with more than 90% of sessions labelled as creating or modifying code showing code changes; the expertise and success classifiers are illustrated against SWE-chat, a public dataset of coding-agent sessions. The authors nonetheless state that classifiers "remain challenging to validate at scale," and that Claude Code sessions may be too long and complex for human labels to serve as ground truth.

Success itself is a transcript-derived construct in two layers. *Judged success* comes from a classifier deciding whether the person did what they set out to do; *verified success* additionally requires at least one hard verifiable signal — git commits or pull requests matching the work, passing test suites, or explicit affirmation from the user. Sessions judged to have no clear goal, about 7.7% of the sample, are excluded from the outcome analysis. Expertise comparisons hold work mode, task-value band, month, task subject, and broad occupation group fixed, which the authors offer as a partial rather than complete answer to the concern that experts simply pick different tasks.

The stated limitations are that real-world outcomes are unobserved — whether code from a session is actually used or discarded is not measured — and that non-interactive usage, described as a substantial share of activity, is excluded entirely, with a framework to measure it named as a priority for future work. The authors also name two future signals they intend to watch: returns to expertise beginning to fall, which would suggest models are starting to supply the judgment users currently bring; and continued growth in successful coding sessions by users outside software occupations, which would suggest software production is becoming part of ordinary work in every field.
