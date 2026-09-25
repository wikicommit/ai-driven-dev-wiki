---
title: "Empirical studies of agent-authored pull requests"
lang: en
kind: comparison
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
derived_from:
  - path: .wikicommit/entity/en/ScholarlyArticle/aidev.md
    source_commit: 2021b2ccebc691de4b3f1fac3575b82510221c8e
  - path: .wikicommit/entity/en/Dataset/aidev.md
    source_commit: 4f24561db04e0d1d4e76ad45ceeafcc734f1123b
  - path: .wikicommit/entity/en/ScholarlyArticle/why-are-agentic-pull-requests-merged-or-rejected.md
    source_commit: 4f24561db04e0d1d4e76ad45ceeafcc734f1123b
  - path: .wikicommit/entity/en/ScholarlyArticle/where-do-ai-coding-agents-fail.md
    source_commit: fb81a1a633a4538dec7293228db126d1e781d8ff
  - path: .wikicommit/entity/en/ScholarlyArticle/how-ai-coding-agents-modify-code.md
    source_commit: 864e0a92b6b7213d87ef534b8204d9992ffc5386
  - path: .wikicommit/entity/en/ScholarlyArticle/how-do-ai-coding-agents-contribute-to-software-development.md
    source_commit: 59f94553fa52912f703987f31c807ff6a3208a7d
  - path: .wikicommit/entity/en/ScholarlyArticle/these-arent-the-reviews-youre-looking-for.md
    source_commit: 67eb2a7e7aeea32abb49ca81daa984b78b394440
  - path: .wikicommit/entity/en/ScholarlyArticle/from-industry-claims-to-empirical-reality.md
    source_commit: d6b740fcefb776ad598c9c610d08c7220255d861
  - path: .wikicommit/entity/en/ScholarlyArticle/ai-ides-or-autonomous-agents.md
    source_commit: 864e0a92b6b7213d87ef534b8204d9992ffc5386
---

Six studies in this wiki take pull requests written by AI coding agents on GitHub — [[DefinedTerm/agentic-pull-request]]s — and ask what happened to them: whether they were merged, who reviewed them, how they changed code, and what adopting an agent did to a repository. A seventh sets out the same kind of question without, on its page here, reporting figures. All seven draw on one dataset, [[Dataset/aidev]], yet they cut it differently, count different things as the outcome, and read the same silences in the record in different ways. This page sets them side by side so that those differences are visible; it does not rank the studies or combine their numbers.

## The shared base

[[ScholarlyArticle/aidev]] (MSR '26) introduces AIDev as 932,791 agent-authored pull requests from 116,211 repositories and 72,189 developers, written by five agents — [[SoftwareApplication/openai-codex]], [[SoftwareApplication/devin]], [[SoftwareApplication/github-copilot]], [[SoftwareApplication/cursor]] and [[SoftwareApplication/claude-code]] — with a cutoff of 1 August 2025. A curated subset of 33,596 pull requests from 2,807 repositories with more than 100 stars carries the review comments, commit diffs, issue links and event timelines that the full set lacks. The paper describes the dataset and proposes research questions — on adoption, code-patch characteristics, testing, review dynamics and failure patterns — rather than answering them. The studies below are, in effect, answers to some of those questions.

## The studies side by side

| Study | Venue | Slice of AIDev | Question | Method |
|---|---|---|---|---|
| [[ScholarlyArticle/where-do-ai-coding-agents-fail]] | MSR 2026 (short paper) | All 33,596 curated PRs; 600 rejected PRs coded by hand | Which PR characteristics predict merge, and why are agentic PRs rejected | Cliff's delta, logistic regression, four-level rejection taxonomy |
| [[ScholarlyArticle/why-are-agentic-pull-requests-merged-or-rejected]] | MSR '26 | 11,048 closed PRs in repositories with at least 500 stars, narrowed to 9,799 with human comments; 717 inspected by hand | Do merge and rejection labels reflect agent capability | Two annotators per PR, coding interaction artifacts |
| [[ScholarlyArticle/how-ai-coding-agents-modify-code]] | MSR '26 | 24,014 merged agentic and 5,081 merged human PRs from the MSR 2026 Mining Challenge version | How agentic and human PRs differ in structure, and how well descriptions match diffs | Mann–Whitney U, Cliff's delta, lexical and embedding similarity |
| [[ScholarlyArticle/these-arent-the-reviews-youre-looking-for]] | EASE 2026 (short paper) | Agent- and human-authored PRs in repositories with at least 100 stars, compared within the same repositories | How humans review agent-authored PRs | Rule-based classifier of review comments (96.5% accuracy on a validation sample) |
| [[ScholarlyArticle/from-industry-claims-to-empirical-reality]] | MSR '26 | 3,109 PRs reviewed by actual code review agents, of which 2,456 in the Commented review condition | Does reviewer composition relate to merge outcome | Chi-squared test, keyword-based [[DefinedTerm/signal-to-noise-ratio]] |
| [[ScholarlyArticle/ai-ides-or-autonomous-agents]] | MSR '26 | AIDev v3, with PRs re-parsed from January 2024 to November 2025; 401 agent-first and 117 IDE-first repositories with matched controls | What adopting a coding agent does to repository velocity and quality | Staggered difference-in-differences with propensity-score matching, SonarQube metrics |
| [[ScholarlyArticle/how-do-ai-coding-agents-contribute-to-software-development]] | arXiv (2607.21832) | AIDev | How merge rates, task types and PR characteristics of agentic and human PRs change over development quarters | Longitudinal comparison |

## Where they differ

### What counts as the outcome

Three of the studies treat the merge decision as the thing to explain, and they do not treat it the same way; a fourth looks only at merged PRs.

- [[ScholarlyArticle/where-do-ai-coding-agents-fail]] treats merged versus not merged as the outcome and asks what predicts it. Across the 33,596 curated PRs it reports 71.48% merged, and finds each additional failed CI check reduces the odds of merge by about 15% — the largest single effect it measured.
- [[ScholarlyArticle/why-are-agentic-pull-requests-merged-or-rejected]] questions whether that outcome measures agent capability at all. Of 353 rejected PRs it inspected, 35.7% showed observable agentic failure, 31.2% were closed for workflow reasons such as duplicates or superseded changes, and 33.1% could not be classified. Of 364 merged PRs, 15.4% involved explicit reviewer participation. Its authors argue that outcome-based metrics conflate agent capability with repository workflows.
- [[ScholarlyArticle/from-industry-claims-to-empirical-reality]] uses merge as the outcome of a different variable — who reviewed the PR — and reports 45.20% merged for PRs reviewed only by code review agents against 68.37% for PRs reviewed only by humans. Its authors state that the chi-squared result establishes association, not causation.
- [[ScholarlyArticle/how-ai-coding-agents-modify-code]] does not model the outcome: it keeps only merged PRs and compares their structure.

[[ScholarlyArticle/ai-ides-or-autonomous-agents]] moves the unit from the pull request to the repository-month. Its outcome is what a repository's commits, lines added, static-analysis warnings and cognitive complexity do after its first agent-generated PR.

### How silence in the record is read

A pull request that closes or merges with no recorded human comment turns up in three studies, each of which handles it differently.

- [[ScholarlyArticle/where-do-ai-coding-agents-fail]] counts "reviewer abandonment" — a PR closed with no meaningful human interaction — as a rejection pattern, the most common one in its taxonomy (228 PRs, 38% of its coded sample).
- [[ScholarlyArticle/why-are-agentic-pull-requests-merged-or-rejected]] places silent closures in an "unknown" category rather than a cause, and argues that evaluation should represent that uncertainty explicitly. It also removed PRs with no human comments before sampling.
- [[ScholarlyArticle/these-arent-the-reviews-youre-looking-for]] classifies every PR without comments as not reviewed, while stating that this does not establish the absence of oversight, because a maintainer may inspect a PR without leaving a trace. On that basis it reports that 61.38% of the 33,596 agent-authored PRs received no recorded review.

### Comparing agents with humans

Three studies put agent-authored PRs against human-authored ones, and each compares a different property.

- [[ScholarlyArticle/how-ai-coding-agents-modify-code]] compares code structure: agentic PRs make smaller, more localized edits across fewer files and commits, with commit count showing the largest difference (Cliff's δ = 0.5429). Their descriptions match their diffs slightly more closely than human ones on all four similarity measures.
- [[ScholarlyArticle/these-arent-the-reviews-youre-looking-for]] compares review: within the same repositories, observable human participation is nearly identical (30.1% for agent-authored PRs against 30.8% for human-authored ones), but its form differs. [[DefinedTerm/agent-steering]] makes up 25.92% of human comments on agent-authored PRs against 1.63% on human-authored ones.
- [[ScholarlyArticle/how-do-ai-coding-agents-contribute-to-software-development]] compares merge rates, task types and PR characteristics over development quarters. Its page in this wiki records its questions and design but not its figures.

### Comparing agents with each other

Where the studies break results down by agent, the five agents do not behave alike.

- [[ScholarlyArticle/where-do-ai-coding-agents-fail]] reports merge rates from 82.59% for OpenAI Codex down to 43.04% for GitHub Copilot, with Cursor, Claude Code and Devin between them.
- [[ScholarlyArticle/why-are-agentic-pull-requests-merged-or-rejected]] finds that Copilot and Devin account for 54 of the 56 merged PRs in its sample that needed a feedback loop or human intervention, while Codex and Cursor PRs were typically merged with minimal interaction. It attributes this partly to the repositories those agents are used in, such as stricter CI gating, so the observed outcome reflects the deployment context as much as the agent.
- [[ScholarlyArticle/how-ai-coding-agents-modify-code]] reports that Claude Code and Codex show wider variability in change size, while Devin, Cursor and especially Copilot produce consistently small, localized changes.

### Rejection causes

The two studies that code rejected PRs by hand use different schemes and so cannot be read against each other number for number.

- [[ScholarlyArticle/where-do-ai-coding-agents-fail]] uses four levels — Reviewer, Pull Request, Code and Agentic — and finds agent-level causes the rarest (13 PRs, 2%): the agent repeatedly ignoring reviewer instructions, or violating a contribution policy. Duplicate PRs (23%) and CI/test failures (17%) are the largest patterns below reviewer abandonment.
- [[ScholarlyArticle/why-are-agentic-pull-requests-merged-or-rejected]] uses three categories for rejected PRs — agentic failure, non-agentic failure, unknown — and counts failing checks or tests as signals of agentic failure.

Failing CI therefore sits at the Code level in one scheme and counts as agentic failure in the other.

### Velocity and quality

[[ScholarlyArticle/ai-ides-or-autonomous-agents]] is the only study here that measures what happens to a repository over time, and it splits repositories by prior AI tool use. Where the agent was the first observable AI tool, commits rose 36.3% and lines added 76.6% on average after adoption. Where an AI IDE came first, gains were short-lived and later turned negative. Static-analysis warnings (about +18%) and cognitive complexity (about +39%) rose in both groups. Its authors call the accumulating complexity agent-induced complexity debt.

## How each study handled the dataset's labels

Several studies did not take AIDev's labels as given, and each corrected something different.

- [[ScholarlyArticle/these-arent-the-reviews-youre-looking-for]] removed 1,044 PRs labelled human-authored that were in fact created by agents, and corrected review comments whose account type was misrecorded.
- [[ScholarlyArticle/from-industry-claims-to-empirical-reality]] had to classify `Bot` accounts by hand, because that type covers CI/CD runners as well as code review agents.
- [[ScholarlyArticle/ai-ides-or-autonomous-agents]] re-attributed PRs to agents from branch prefixes, author logins, commit authors and co-authorship strings, and reports that this surfaced misclassifications and missing PRs in the original dataset.
- [[ScholarlyArticle/how-ai-coding-agents-modify-code]] reconstructed commits and diffs for human PRs through the GitHub REST API, because the version it used lacked commit-level data for them.

## What they share as limits

The studies state their own limits, and most of them overlap:

- Findings are limited to open-source GitHub repositories and the five agents AIDev covers.
- Several studies further restrict to repositories above a star threshold.
- A recorded interaction is not the same as the reasoning behind a decision.

[[Dataset/aidev]] notes the same boundary for the dataset itself: nothing drawn from it extends automatically to proprietary repositories, other platforms, other agents, or activity after its cutoff.
