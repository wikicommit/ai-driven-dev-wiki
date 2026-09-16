---
title: "Where Do AI Coding Agents Fail? An Empirical Study of Failed Agentic Pull Requests in GitHub"
type: "schema:ScholarlyArticle"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2601.15195'
    hash: sha256:b0a9c41c51d96f878d99ca75c0077e291910cdfd54abe16f5227995804be01cd
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A large-scale empirical study of 33,596 pull requests authored by five AI coding agents across GitHub, quantifying which task types and PR characteristics predict merge success, and deriving a hierarchical taxonomy of why agentic PRs get rejected."
  author: ["Ramtin Ehsani", "Sakshi Pathak", "Abdullah Al Mujahid", "Mia Mohammad Imran", "Shriya Rawal", "Preetha Chatterjee"]
  datePublished: "2026-01-21"
  keywords: ["Agents", "Large language models", "Agentic pull request", "AIDev"]
---

This paper reports a large-scale empirical study of 33,596 pull requests authored by five AI coding agents (OpenAI Codex, GitHub Copilot, Devin, Cursor, Claude Code) across GitHub repositories with over 100 stars, using the AIDev-pop dataset. It addresses two research questions: how merged and not-merged agentic PRs differ across task type, code-change size, CI outcomes, and review dynamics (quantitative, the full 33,596-PR dataset), and what specific patterns cause agentic PRs to be rejected (qualitative, a manually-coded sample of 600 rejected PRs).

Its central finding is that agentic PR failure is driven at least as much by socio-technical factors — reviewer abandonment, duplicate work, misalignment with what maintainers actually wanted — as by technical defects in the code itself.

## Key Points

- Across all 33,596 PRs, 71.48% were merged; OpenAI Codex contributed the most PRs (21,799) and had the highest merge rate (82.59%), while Copilot had the lowest merge rate (43.04% of 4,970 PRs). Cursor, Claude Code, and Devin had merge rates of 65.22%, 59.04%, and 53.76% respectively.
- Merge rates varied sharply by task type: documentation (84%), CI (79%), and build (74%) tasks merged most often across agents, while performance (55%) and fix (64%, i.e. bug-fix) tasks merged least often.
- Using Cliff's delta effect-size analysis (chosen over significance testing given the dataset's size), not-merged PRs showed a small-to-medium effect toward larger changes (17% for lines-of-code changed, 10% for files changed) and a moderate effect toward more CI failures (24%); logistic regression found each additional failed CI check reduced the odds of merge by about 15%, the largest single effect among the metrics tested.
- From manual coding of 600 rejected PRs (562 after excluding 38 no-longer-accessible ones) into a four-level taxonomy (Reviewer, Pull Request, Code, Agentic), reviewer-level abandonment — a PR closed with no meaningful human interaction — was the single most common rejection pattern, accounting for 228 PRs (38%).
- Within Pull-Request-level rejections (188 PRs, 31%), duplicate PRs were the largest single pattern (142 PRs, 23%), where maintainers explicitly pointed to another PR already implementing the same change.
- Within Code-level rejections (133 PRs, 22%), CI/test failure was the dominant pattern (99 PRs, 17%), ahead of incorrect implementation (19 PRs, 3%) and incomplete implementation (15 PRs, 2%).
- Agentic-level rejections were the rarest category (13 PRs, 2%): 9 PRs showed the agent repeatedly failing to follow explicit reviewer instructions across multiple feedback rounds, and 4 involved licensing/contribution-policy violations (e.g. not signing a CLA).
- The taxonomy's inter-rater reliability (Cohen's kappa) rose from 0.55 on an initial 50-PR round to 0.91 across the full 100-PR calibration set after the coders discussed disagreements and added a fourth ("Agentic") category, before being applied independently to 500 more PRs.

## Notes

The study's dataset (AIDev-pop) and its 11 task-type labels are drawn from prior published work the authors cite, not constructed by this paper. The qualitative taxonomy and its 600-PR sample are this paper's own contribution; the 33,596-PR quantitative dataset is the full population available in AIDev-pop at the time of the study, not a further sample. The paper is a short (5-page) MSR 2026 conference paper rather than a full journal-length study.
