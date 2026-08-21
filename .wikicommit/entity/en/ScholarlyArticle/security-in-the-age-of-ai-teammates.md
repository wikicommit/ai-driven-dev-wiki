---
title: "Security in the Age of AI Teammates: An Empirical Study of Agentic Pull Requests on GitHub"
type: "schema:ScholarlyArticle"
lang: en
tags: [agentic-coding, security, empirical-study, code-review, metrics]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2601.00477'
    hash: sha256:8560fa76d611e9a921b31427351f87a9a7158991b870734157262fb948a9a3fb
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An empirical study of 33,596 agent-authored pull requests from the AIDev dataset, identifying 1,293 security-relevant ones (3.85%). It finds that agents' security work is mostly hardening rather than vulnerability fixing, that merge rates vary widely by agent, and that human reviewers subject security PRs to markedly longer scrutiny — a median 3.92 hours against 0.11."
  author:
    - "Mohammed Latif Siddiq"
    - "Xinye Zhao"
    - "Vinicius Carvalho Lopes"
    - "Beatrice Casey"
    - "Joanna C. S. Santos"
  datePublished: "2026-01-01"
---

"Security in the Age of AI Teammates" is an empirical study by five authors at the University of Notre Dame, posted to arXiv on 1 January 2026. Its subject is what autonomous coding agents actually do about security when they author pull requests against real repositories, and how human maintainers respond.

The gap it identifies is that prior empirical work on agent-authored pull requests has concentrated on productivity and acceptance rates, "leaving the role of autonomous agents in software security and the dynamics of human review largely unexplored." Its data is the AIDev dataset of 33,596 curated pull requests authored by five widely deployed autonomous coding agents, from which security-relevant PRs are identified by rule-based filtering and then manually confirmed.

## Key Contributions

- **Prevalence, and its uneven distribution.** 1,293 confirmed security-relevant agentic pull requests, or 3.85% of all agent activity in the dataset. The share differs sharply by agent: [[SoftwareApplication/claude-code]] shows the highest proportion at 459 PRs, 14.6% of its own activity, followed by Copilot at 4,970 PRs (10%) and Devin at 4,827 PRs (7.6%) — far larger absolute numbers at lower rates. OpenAI Codex sits at the other end, with only 1.3% of its PRs confirmed as security-relevant after manual validation.
- **Security work is mostly hardening, not vulnerability fixing.** The paper's classification splits security-relevant PRs into four mutually exclusive categories — dependency update, vulnerability fix, security feature, and configuration/compliance — and its finding is that "rather than focusing solely on narrow vulnerability fixes, agents most frequently perform supportive security hardening activities, including testing, documentation, configuration, and improved error handling." Its qualitative analysis of PR titles and descriptions adds that security work is often embedded within broader development goals, most commonly code refactoring and functionality improvement, rather than being undertaken as security work in its own right.
- **Acceptance varies widely by agent and by language.** Merge rates for security-related agentic PRs range from 49.60% for Copilot to 86.59% for OpenAI Codex. By ecosystem, Rust security PRs show the lowest acceptance at 51.16%.
- **Security PRs receive markedly heavier human scrutiny.** Median review latency is **3.92 hours for security PRs against 0.11 hours for non-security ones** — a roughly 36× difference in the median. The paper reports 1,130 security PRs against 30,154 non-security ones in this comparison, and the gap holds alongside lower merge rates for the security set.
- **What predicts rejection is not security content.** The paper's analysis of early PR-level signals finds that "perceived risk is more strongly linked to complexity and verbosity (e.g., longer titles) than to explicit security terminology." Its conclusion draws the implication directly: "security review of agent-authored code extends beyond vulnerability content alone and is shaped by contextual and cognitive factors."

## Notes

The review-latency contrast is the result with the widest implications for practice, because it quantifies something that is otherwise only anecdotal: the human review bottleneck is not uniform across agent output. A median of 0.11 hours for non-security agentic PRs — under seven minutes — describes review that is effectively perfunctory, while the same maintainers spend more than three and a half hours on the median security PR. That pattern is consistent with the review-cost findings recorded on [[DefinedTerm/verification-bottleneck]], and it sharpens them: reviewers appear to be triaging rather than reviewing uniformly, which means the categories they *fail* to flag as security-relevant get the seven-minute treatment.

The rejection-signal finding is the paper's most uncomfortable one, since it suggests review decisions track how much work a PR looks like rather than how risky it is. Read with the previous point, the picture is of a review process responding to surface cues.

Two boundaries apply. The measurements are of pull-request outcomes and review timing rather than of security outcomes — nothing here establishes whether the merged security PRs were correct or whether the rejected ones should have been merged. And identification of "security-relevant" rests on rule-based filtering with manual confirmation over PR content and dataset tags, so the prevalence figure is a floor on work that reads as security-related, not a measure of security-relevant change in general.
