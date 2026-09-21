---
title: "AI-to-AI Code Reviews of GitHub Pull Requests"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-code-review, agents, mining-software-repositories]
sources:
  - type: url
    url: 'https://arxiv.org/html/2608.21311v1'
    hash: sha256:fbf82284375303f9675600e80d90e76d55be064a407f52c9123f292427a990b4
    license: CC-BY-4.0
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A large-scale characterization of pull requests authored by one AI coding agent and reviewed by another, built by attributing GitHub events to specific agent products. It reports the scale and rapid growth of the phenomenon and finds reviewer output varying with which agent wrote the code, while declining to read any of it as a measure of code quality."
  author: ["Niruthiha Selvanayagam", "Taher A. Ghaleb"]
  datePublished: "2026-08-21"
  abstract: "AI coding agents now operate on both sides of the pull request, as authoring agents that create or modify PRs and as reviewers that evaluate them, creating a closed loop in which one agent reviews another's contribution. The paper constructs an AI-to-AI code review dataset by linking AI-authored PRs with AI-attributed review events from CodAGE, and measures reviewer behaviour through CodeRabbit comment categories, per-PR comment volume, and time to first review across author–reviewer pairings."
  keywords: ["AI coding agents", "AI code review", "closed-loop AI", "Pull requests", "Mining software repositories", "GitHub events"]
---

This paper asks how often AI coding agents review other AI coding agents' pull requests on public GitHub, and whether what a reviewer produces depends on which agent wrote the code. It builds its population by applying a two-tier signature attribution method to [[Dataset/codage]], a public dataset of coding-agent GitHub events drawn from GHArchive, and links AI-authored PRs to AI-attributed review events over 2024–2026. The resulting dataset covers 248,641 unique AI-attributed PRs that received at least one AI-attributed review, of which 45,269 were reviewed across products and 208,145 within the same product; 4,773 received both.

On prevalence, the paper's finding is that [[DefinedTerm/closed-loop-ai-review]] is a minority of agent activity but already large in absolute terms, and growing steeply. On reviewer behaviour, it holds [[SoftwareApplication/coderabbit]] constant as the reviewer and varies the authoring agent, then separately contrasts same-product against cross-product pairings on per-PR comment volume and on time from PR creation to first review.

The paper is unusually careful about what its numbers do not show. Counts are presented as lower bounds conditioned on signature attribution; the reviewer-output measures are CodeRabbit's own self-declared comment categories rather than validated defect labels; and the same- versus cross-product comparisons are framed as observational, with change size, language, repository and reviewer composition named as uncontrolled. It appears in the Emerging Results, Vision & Reflection track of the 20th International Symposium on Empirical Software Engineering and Measurement (ESEM 2026), held 8–9 October 2026 in Munich, as arXiv:2608.21311v1 under CC BY 4.0, with work partially supported by NSERC grant RGPIN-2025-05897 and a replication package at <https://github.com/Niruthiha/AI-AI-CodeReviews>.

## Key Points

- The paper defines "closed-loop AI review" in an observable sense only: AI occupies both sides of the pull request. Because the review stream is restricted to AI-attributed events, it explicitly does not mean humans were absent, and a PR in the dataset may also have had human review that was not observed.
- Of 2,830,284 agent-authored PRs identified, 248,641 (8.8%) received at least one AI review; 45,269 (1.6%) were reviewed across products, spanning 10,345 repositories.
- Cross-product closed-loop review grew from 57 PRs in 2025-Q1 to 25,492 in 2025-Q3, and same-product from 40 to 57,080 — more than two orders of magnitude in both cases. 2025-Q4 counts are treated as lower bounds because GHArchive attributes lag event data by about a quarter.
- Attribution is two-tier: a high-confidence body signature (such as a `Co-Authored-By` trailer or a vendor agent URL in the PR body) or an exact match on a vendor-controlled login (such as `coderabbitai[bot]`). Branch-name prefixes are recorded but never sufficient on their own, being user-controllable.
- That strictness is costly on the author side: 38.0% of candidate PRs were quarantined, 96.9% of them because only a branch name matched — so the agent-authored population is the 62.0% carrying a body or login signature, not everything a looser rule would admit.
- OpenAI Codex dominates as a cross-product author (31,601 PRs, 69.8% of the cross-product set) and Copilot as a reviewer (21,022 of 47,259 author–reviewer pairs); the modal pairing is Codex authored, Copilot reviewed, at 18,114 pairs.
- Whether an agent is reviewed by its own product is sharply non-uniform: Copilot (95.7%), Amazon Q (91.8%) and Devin (76.5%) are reviewed mostly within their own product; OpenAI Codex is balanced at 54.1%; and Cursor (0.0%), Google Jules (0.0%) and Claude Code (0.5%) are reviewed almost entirely across products.
- With CodeRabbit held constant as reviewer, its comment-category mix differs by authoring agent: 35.0% of comments on Claude Code PRs are labelled refactor against 10.5% on Copilot PRs, a 24.5 percentage-point difference (95% CI [23.1, 25.9]). The overall association is statistically significant but small (Cramér's V = 0.150).
- The paper states plainly that this difference may stem from the PRs themselves rather than from the reviewer, and makes no claim about code quality.
- Three of four dual-role reviewers produced 58–65% more comments per PR on same-product PRs (Copilot 1.49 → 2.35, Devin 1.09 → 1.80, Amazon Q 4.94 → 8.08), with OpenAI Codex the exception at 0.91 vs 0.89. Effect sizes were small to negligible (Cliff's delta 0.02–0.27) and the gap is attributed to a long right tail rather than a population-wide shift.
- Among pairs with complete, nonnegative timestamps, median time from PR creation to first AI review was 1.2 minutes cross-product and 4.7 minutes same-product — the opposite of a "product rubber-stamps its own" reading. The paper attributes this to composition: fast reviewers such as Gemini Code Assist (0.5 min median) are commoner cross-product, while Copilot (17.7 min median) dominates the same-product set.
- Timestamp completeness differed sharply between the groups — 79.2% of cross-product pairs retained against 31.9% of same-product pairs — which the paper gives as a reason to read the latency comparison descriptively only.
- Same- and cross-product are defined at the level of the identifiable agentic product or harness, not the parent company or the underlying model: Google Jules and Gemini Code Assist are treated as distinct products despite a shared vendor, accounting for 117 of the 45,269 cross-product PRs.
- The study analyses no matched human-authored control group, and compares its latency figures against no human baseline.

## Notes

The paper positions itself against two existing lines of work: studies of agent-authored PRs, which ask whether agent-written code is accepted, and studies of reviewer-side bots, which predate the current ecosystem of dual-role agents. What it claims as new is product-resolved author–reviewer pairing at scale — which agents review which others, and whether observable behaviour differs between same- and cross-product configurations.

Its own stated limitations are extensive. Attribution can undercount agents whose signatures are missing, uncatalogued, or stripped by squash merges, and under-attribution is asymmetric: lower on the reviewer side, where major reviewers post under vendor-controlled bot logins, than on the author side, which depends on body trailers. The absence of a signature is not evidence that a PR was not AI-authored or AI-reviewed — such PRs never enter the population at all. Coverage is public GitHub only, excluding private repositories, GitHub Enterprise and other platforms, and is conditioned on repositories that adopt these integrations.

The future work the authors set out is mostly about what this method cannot reach. They call for human annotation of review comments for correctness, localization, severity and actionability, with outcome linkage to accepted suggestions, later commits, CI results, merges and reverts, since comment volume and category mix do not show whether a review improved the code. They also note that product-level attribution is not model-level attribution, so same-product and cross-product are not same-model and different-model — a distinction that matters because, as they observe from work outside software engineering, model evaluators may favour outputs resembling their own. Testing whether AI authors and reviewers share correlated blind spots would need a controlled benchmark with injected defects, which public records cannot supply.
