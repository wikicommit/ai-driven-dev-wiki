---
title: "Agentic Pull Request"
type: "schema:DefinedTerm"
lang: en
aliases: ["Agentic-PR", "Agentic PR"]
tags: [coding-agents, code-review]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.22534'
    hash: sha256:86242f871d4dd502cdfdf9c5a6346361f31b07c300cce562052319a0eb42cb18
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A pull request submitted to a software repository by an AI coding agent rather than by a human developer, used in empirical software engineering research as the unit for studying how agent-authored changes are reviewed, merged or rejected."
---

An agentic pull request (Agentic-PR) is a pull request submitted to a repository by an AI coding
agent, so that the agent participates directly in real-world software development.
[[ScholarlyArticle/why-are-agentic-pull-requests-merged-or-rejected]]
uses the term for agent-authored PRs to open-source repositories, drawing on evidence from the
[[Dataset/aidev]] dataset that such PRs span thousands of repositories, and treats a *closed*
Agentic-PR as one that received an explicit merge or rejection decision.

## Usage

The term is used in mining-software-repositories research as the unit of analysis for studying how
agent-authored changes fare once they meet human reviewers. In that study's account, Agentic-PRs
are commonly evaluated with outcome-based measures such as merge rates or approval frequencies, and
the study's central claim is that those outcomes misrepresent agent capability on their own: a
rejection may reflect a workflow constraint or an undocumented reviewer decision rather than an
agent failure, and a merge may depend on reviewer feedback or commits applied by a human. In its
manually inspected sample only 35.7% of rejected Agentic-PRs showed clear agentic failures, and
15.4% of merged ones involved explicit reviewer participation.

Because of this, the study separates Agentic-PRs reviewed only by bots from those with human
comments, excluding the former as cases where no human decision context is available, and argues
for interaction-aware evaluation that reads reviewer comments, CI outcomes, commit history and
workflow actions rather than the final PR state alone.

## Related Terms

- [[DefinedTerm/ai-coding-agent]]
- [[DefinedTerm/agentic-code-review]]
- [[DefinedTerm/review-bottleneck]]
