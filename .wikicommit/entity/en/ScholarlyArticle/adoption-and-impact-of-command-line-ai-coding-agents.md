---
title: "Adoption and Impact of Command-Line AI Coding Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: [coding-agents, adoption, productivity, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2607.01418'
    hash: sha256:bbc1053e3b6e6a0aa7c93d9962cf8cb956ef31b8a516dbcb70bf3743e8cbf04d
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Microsoft field study of the company's early-2026 rollout of Claude Code and GitHub Copilot CLI, using developer-level telemetry from tens of thousands of engineers to examine who adopts command-line AI coding agents, who keeps using them, and whether adopters merge more pull requests."
  author: ["Emerson Murphy-Hill", "Jenna Butler", "Alexandra Savelieva"]
  abstract: "Studying tens of thousands of Microsoft engineers over the company's early-2026 rollout of agentic command-line tools, the paper finds that first use spread primarily through social networks, that retention was associated more with engineers' coding activity than with demographics, and that adopters merged roughly 24% more pull requests than they would have otherwise, with the lift persisting across a four-month window. It concludes that CLI coding agents are neither uniformly adopted nor mere novelty effects and that organisations should treat visible peer use as central to rollout strategy."
  keywords: ["agentic command line tools", "developer AI adoption", "retention", "merged pull requests", "telemetry"]
---

This paper by Emerson Murphy-Hill, Jenna Butler and Alexandra Savelieva of
[[Organization/microsoft]] studies Microsoft's early-2026 experience of offering its engineers two
agentic command-line tools, [[SoftwareApplication/claude-code]] and
[[SoftwareApplication/github-copilot-cli]]. It frames three concerns that follow any such rollout —
which engineers will adopt, whether they will keep using the tool, and whether it produces enough
additional output to justify its token cost — and presents itself as the first field study to use
developer-level telemetry to analyse both the adoption of agentic command-line tools and their effect
on pull-request output. The authors contrast this with prior adoption work, which they describe as
resting on surveys, interviews or lab tasks, and with prior impact work that infers AI use from
public-repository signals such as commit co-author trailers, where a "non-adopter" may simply be
someone whose use left no trace.

The work has two parts. An adoption study covers only Copilot CLI, the tool with a well-defined
eligible population at rollout: it models first use as a discrete-time hazard on an engineer-week
panel and retention (activity on at least 5 of the 14 days from first use) with logistic regression,
using predictors for social exposure, prior IDE Copilot use, baseline pull-request activity, career
stage and tenure. An outcomes study covers both tools and measures merged pull requests, first with a
synthetic-control counterfactual built with CausalImpact and then with within-person fixed-effects
models. January 5, 2026 is treated as the rollout date, with observation windows closing on April 29,
2026, and an internal survey of 609 attendees of an "Agentic Engineering Day" is used to help
interpret the results.

## Key Points

- Adoption was substantially social: an engineer whose skip-level peers were largely using Copilot
  CLI had 216% higher odds of trying it (where more than a quarter had), the strongest signal found;
  a direct manager's use was associated with 82% higher odds of trying it and 22% higher odds of
  sticking with it.
- Prior IDE Copilot use cut in opposite directions: it raised the odds of trying Copilot CLI (up to
  83% at 60+ days of prior use) but was associated with lower retention (between −12% and −15%),
  which the authors interpret as engineers having a familiar fallback.
- Busier engineers were more likely both to try and to keep using Copilot CLI, while career stage
  and tenure mattered little — the authors conclude that what an engineer does explains adoption and
  retention far better than who they are in the organisation.
- CausalImpact estimated a +24.0% lift in merged PRs per engineer per day over the post-period (95%
  CI +14.5% to +33.7%) for early adopters, and the lift showed no statistically distinguishable
  decay across the four-month window; a placebo intervention returned −1.1%.
- Within-person, the merged-PR lift rose with how many days a week the tools were used, from +15.0%
  at three days to +50.1% at five or more, which the authors read as an association rather than a
  cause.
- Among single-tool users, weeks of Copilot CLI use showed a +24.9% lift against +11.4% for Claude
  Code, about 2.2 times larger. The authors call this surprising given public sentiment favouring
  Claude Code and offer two hypotheses: different task mixes, and Microsoft's ownership of GitHub
  helping align the Copilot CLI harness with how its engineers work.

## Notes

The authors state that merged pull requests are an imperfect proxy for output that rewards small,
frequent PRs and may miss quality costs; that the adoption study cannot separate peer influence from
homophily; that findings come from one company in a single early-2026 window and count only Azure
DevOps pull requests; and that, as Microsoft employees, their proximity to a company that sells AI
tools and owns GitHub may have shaped the work. They name quality — whether the added throughput
yields better software — as the pressing open question. They disclose using GitHub Copilot, predominantly with
Anthropic Claude Opus models, to draft an initial version of the manuscript, to implement the
analysis and figure-generating code, and to assist with reorganisation and copy-editing, while
stating that the research questions, designs and interpretations are their own.
