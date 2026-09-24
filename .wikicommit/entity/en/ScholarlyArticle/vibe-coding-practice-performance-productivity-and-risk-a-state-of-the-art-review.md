---
title: "Vibe Coding: Practice, Performance, Productivity, and Risk—A State-of-the-Art Review"
type: "schema:ScholarlyArticle"
lang: en
tags: [vibe-coding, survey, productivity, security, ai-assisted-programming]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2608.20446'
    hash: sha256:0da04778d6078d3c6ebfb0bd3fb744c0556b4478345788965c0057741da1e41a
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A cross-disciplinary state-of-the-art review of the first seventeen months of evidence on vibe coding, covering models and tools, benchmark performance by task type, productivity, and risk."
  author: ["Dominik L. Michels", "Mutaz Abu Ghazaleh", "François Lazzari", "Nabil Kassem", "Jonathan Klein"]
  abstract: "Vibe coding — AI-assisted software development in which the developer describes intent in natural language and validates results by running rather than reading the generated code — was named in February 2025 and produced its first body of empirical evidence within seventeen months. The review assembles that evidence across software engineering, human–computer interaction, labour economics, security research, governance and education, surveying the model landscape, tool ecosystem and performance by task type. It argues that an apparently contradictory productivity record (+26% more tasks per week, a 19% slowdown, code-review time up 441%) is consistent once measurement method, scope and time horizon are held constant, identifies six patterns behind the dispersion, documents security failures, code-quality degradation, unsettled copyright exposure and skill atrophy, and closes with open questions and a falsifiable conjecture that the gains are real on new code and shrink or reverse on mature codebases."
  keywords: ["vibe coding", "AI-assisted software development", "productivity", "benchmarks", "security", "skill atrophy"]
---

This review, by authors at KAUST's Computational Sciences Group, MAGTechAI and GNTEQ, surveys what
is known about [[DefinedTerm/vibe-coding]] from a deliberately cross-disciplinary corpus of 123
cited sources spanning software engineering, human–computer interaction, labour economics, security
research, governance and education. It describes itself as a state-of-the-art rather than a
systematic review: coverage is exhaustive for the controlled trials, benchmark results and
telemetry studies its quantitative sections depend on, while for illustrative registers such as
deployment failures and institutional reversals the authors stopped adding cases once a pattern was
established. Sources are organised into evidential tiers — peer-reviewed work and the METR
randomised controlled trial at the top, vendor self-reports and practitioner anecdotes treated as directional
signals needing triangulation — and ephemeral sources are cited through archived snapshots.

For its definition the review adopts the boundary drawn by Simon Willison in a blog post:
what distinguishes vibe coding is not the use of an LLM but the developer's disengagement from the
generated code, validating by whether the output runs rather than by reading it. On that boundary
the conversational-IDE workflow, in which the developer still reviews and tests what the model
writes, falls outside vibe coding proper, while the agentic command-line tools of 2024–2025 moved
the frontier toward autonomous task completion.

## Key Points

- The review finds the early code-generation benchmarks saturated and reads the climb on
  SWE-Bench Verified as qualified by lower scores on contamination-resistant and independently run
  evaluations; it concludes that benchmark scores are evidence of capability under favourable
  conditions, not of reliability in production.
- Decomposing capability by task type, it argues that the decisive variable is verifiability rather
  than difficulty: where a mechanical feedback loop exists (a test suite, a crash, a compiler) the
  systems are strong, and where none exists — the fault-detection strength of generated tests, the
  accuracy of generated documentation, the judgement behind a refactoring — failures are silent and
  expensive to audit. It calls the result reliable code generation alongside weak fault detection
  and hard-to-audit documentation.
- It treats the productivity record as consistent rather than contradictory once measurement is held
  constant, and names six patterns behind the dispersion: effects shrink as measurement broadens;
  self-report diverges from independent measurement; the largest claims describe displacement or
  output volume rather than productivity; headlines are rarely re-tested over longer horizons, and
  those that were have not held; audit quality varies inversely with headline magnitude; and
  seniority findings reconcile only because they measure different quantities.
- It groups the documented dangers into four registers: operational and security failures in
  deployed applications, measurable degradation of code quality and maintainability at population
  scale, unsettled intellectual-property and copyright exposure, and erosion of developer skill and
  the entry-level labour pipeline — risks it argues compound one another.
- It observes open-source maintainers, with no particular reason to coordinate, converging within a
  twelve-month window on the same line: AI as reviewer and analyser is accepted, AI as autonomous
  author is not. It sees enterprise governance, such as Amazon's 90-day code safety reset requiring
  two-person review for critical systems, arriving at the same line from the opposite direction.
- It closes with four open questions — long-term developer comprehension under sustained assistance,
  the multi-year maintenance economics of vibe-coded codebases, the legal status of AI-mediated
  clean-room reimplementation, and the absence of any study stratifying productivity by codebase age
  — and a falsifiable conjecture that the gains are real on new code and shrink or reverse on mature
  codebases, which it says no study in its corpus was designed to test.

## Notes

The review positions itself against two prior surveys of vibe coding that it describes as each
anchored in a single discipline, and frames its central tension as three curves moving in different
directions over the same period — benchmark capability, measured productivity for experienced
developers on mature codebases, and a population-level skill cost — each of which it considers real.
Its authors note that many sources were collected as they appeared, so the corpus preserves claims
in the form first made, several later revised or withdrawn, and that the vendor-produced datasets
it draws on carry a commercial-interest caveat. The paper states that AI assistance (Claude Opus
4.8) was used for drafting text from collected notes, plotting code, online research, and
generating artificial reviews of drafts, with the text subsequently reworked by the authors.
