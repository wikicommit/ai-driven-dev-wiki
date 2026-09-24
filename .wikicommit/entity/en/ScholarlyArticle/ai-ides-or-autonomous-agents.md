---
title: "AI IDEs or Autonomous Agents? Measuring the Impact of Coding Agents on Software Development"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, software-engineering, productivity, technical-debt]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2601.13597'
    hash: sha256:3efb3411cda099a6566dd43fd5ca99be03399777daced6038dbbe0301f2050b2
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A longitudinal causal study of coding-agent adoption in open-source GitHub repositories, finding large front-loaded velocity gains only where the agent was the project's first observable AI tool, but persistent increases in static-analysis warnings and cognitive complexity regardless of prior AI IDE use."
  author: ["Shyam Agarwal", "Hao He", "Bogdan Vasilescu"]
  abstract: "The paper estimates the effect of adopting LLM-based coding agents — defined as a repository's first agent-generated pull request — on monthly repository-level development velocity and software quality, using staggered difference-in-differences with matched controls on the AIDev dataset. It separates repositories with no prior AI IDE traces from those that used AI IDEs before adopting an agent, and finds that velocity gains depend on that prior exposure while quality risks do not."
  keywords: ["Autonomous coding agents", "Agentic AI", "AI-assisted programming", "Software quality", "Longitudinal study", "Causal inference"]
---

This paper asks what happens to an open-source project when it starts accepting pull requests from an autonomous [[DefinedTerm/ai-coding-agent]], and whether the answer depends on the project having already used an AI-assisted IDE. The authors distinguish two paradigms: pre-agentic, IDE-based assistants such as early [[SoftwareApplication/github-copilot]] and [[SoftwareApplication/cursor]], which offer synchronous suggestions a developer accepts or rejects while typing, and coding agents such as [[SoftwareApplication/openai-codex]], [[SoftwareApplication/claude-code]], [[SoftwareApplication/devin]] and the Cursor Agent, which work asynchronously at repository level and contribute whole pull requests. They list four dimensions in which agents differ from assistants — autonomy, scope, planning and interaction — and argue that while IDE assistants have been studied extensively, the real-world effects of repository-level agents remain largely unexplored.

The study builds on the [[Dataset/aidev]] dataset (v3), defining a repository's adoption date as the earliest month containing an agent-attributed pull request. Because AIDev's coverage begins in December 2024 while most agentic tools were released earlier, the authors retrospectively parsed all pull requests from January 2024 to November 2025, and attributed them to agents through a cascade of signals — branch prefixes, pull-request author logins, first-commit author names, GitHub's bot actor type, and for Claude Code, co-authorship strings in pull-request text — reporting that this surfaced misclassifications and missing pull requests in the original dataset. Treated repositories are split into agent-first (AF), with no trace of an AI IDE during the collection period, and IDE-first (IF), where configuration artifacts for GitHub Copilot, Cursor or [[SoftwareApplication/windsurf]] appear in the repository before its first agentic pull request. After propensity-score matching, the samples contain 401 AF repositories matched to 606 controls and 117 IF repositories matched to 73 controls. Effects are estimated with a staggered difference-in-differences design using the Borusyak et al. imputation estimator, with velocity measured as monthly commits and lines added and quality as SonarQube static-analysis warnings, duplicated-line density and cognitive complexity.

The method follows earlier work on Cursor adoption, which the paper summarizes as finding short-term velocity gains but increased technical debt. Their reading of the new results is that autonomous agents amplify that speed–maintainability trade-off: velocity benefits depend on prior AI exposure, but the quality cost does not.

## Key Points

- Velocity gains appear only when the agent is the repository's first observable AI tool. On average, AF repositories see +36.3% commits and +76.6% lines added after adoption; IF repositories see +3.1% and −6.3%.
- The AF gains are front-loaded: roughly +111% commits and +216% lines added in the adoption month, with lines added remaining about +49% to +109% above the counterfactual through six months later.
- IF repositories show only a short-lived bump — commits up 16–28% from the adoption month through two months after — before estimates return to near zero and eventually turn negative, at about −61% lines and −35% commits six months after adoption.
- The authors interpret this as diminishing returns: IF repositories have already absorbed productivity gains from AI IDEs and, being more mature — more starred, forked and active with pull requests — likely face coordination, triage and review overhead that offsets localized agent speed-ups.
- Quality risks are persistent regardless of prior AI exposure: across both groups, static-analysis warnings rise by about 18% and cognitive complexity by about 39%.
- Complexity keeps accumulating over time — in AF repositories from +20.7% in the adoption month to about +49% five months later, and in IF repositories at roughly +15% to +62% through six months. The authors call this agent-induced complexity debt.
- Duplication effects are small and inconsistent, which the authors read as quality risk coming from structural complexity rather than copy-paste proliferation.
- Comment density rises substantially in IF repositories (about +22% on average and over +30% by six months) but not in AF repositories, hinting that teams already using AI IDEs also rely on agents for documentation.

## Notes

The authors note isolated significant pre-treatment coefficients for static-analysis warnings and code complexity, which they do not consider pervasive enough to indicate a sustained pre-trend but describe as concerning and as a limitation of the quasi-experimental design and the underlying data. Their estimates are to be read as intent-to-treat effects of observable agent adoption, since usage intensity and developer-level interaction cannot be measured directly.

From these results they argue that velocity increases alone will not suffice: agent adoption needs to be paired with quality safeguards such as complexity-aware review of agent pull requests, routine refactoring and comprehensive automated tests; teams already using AI IDEs should not assume additive productivity and may deploy agents selectively or for tightly scoped tasks; maintainability metrics should be surfaced in agent planning and prompting; and provenance tracking and transparency of agent-generated changes remain essential.

The paper was published at the 23rd International Conference on Mining Software Repositories (MSR '26), April 13–14, 2026, in Rio de Janeiro, under a Creative Commons Attribution 4.0 license (DOI 10.1145/3793302.3793589). The version extracted here is arXiv:2601.13597v2 [cs.SE], stamped 27 January 2026. All three authors are affiliated with Carnegie Mellon University, and a replication package is published on GitHub.
