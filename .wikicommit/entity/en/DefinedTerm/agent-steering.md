---
title: "Agent Steering"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, agents, human-ai-collaboration, pull-requests]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.02273'
    hash: sha256:730f6134755c88620fbdf3f7484bce3b65c3370345ef9ce8ff858915d757ac84
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A form of human participation in code review in which a developer directs an LLM-based coding agent through imperative commands in a pull request thread, rather than evaluating the change independently."
---

Agent steering is human involvement in a pull request that takes the form of directing a coding agent rather than assessing the code. In the classification used by [[ScholarlyArticle/these-arent-the-reviews-youre-looking-for]], an agent-steering comment pairs an agent's name — Copilot, CodeRabbit, Devin, Claude, Gemini, Sourcery-AI and the like — with an imperative verb such as "run", "fix", "rebase", "test" or "update". Both inline commands (for example, "@coderabbit fix lint failure") and comments that simply open by addressing an agent fall into the category. It is distinguished from automation or CI interaction, whose defining characteristic is that it addresses infrastructure rather than an LLM agent, and from direct human review, which is the residual category covering both substantive evaluative feedback and short process-oriented remarks.

## Usage

The term is used to separate two things that a raw count of human comments on a pull request would otherwise merge: a human evaluating a change, and a human operating an agent that produces one. That separation is the point of the concept. The paper that introduces this classification argues that because both appear in the PR history as human-authored comments, review metrics built on comment counts cannot distinguish oversight from operation, and so overstate how much human evaluation a project's review activity represents.

The category is also what carries that paper's strongest reported contrast. Agent steering accounted for 25.92% of human review comments on agent-authored pull requests but only 1.63% on human-authored ones in the same repositories, a difference with a large effect size (Cramér's V = 0.34). Across agent-authored PRs in popular repositories, 28.37% of human comments were agent-steering.

## When It Applies

Agent steering describes what a human does when the author of the change is itself an agent capable of acting on instructions left in the thread, so the practice presupposes an agent that monitors its own pull request and a review surface that doubles as a command channel. The authors note that reusing PR comments this way has real advantages — it reuses existing infrastructure and shortens feedback loops.

Its failure mode, on the authors' account, is interpretive rather than operational: it blurs the boundary between evaluation and interaction, so that observable review activity no longer corresponds to direct human evaluation. Combined with silent or undocumented review, this reduces the traceability of human oversight in the PR record.

The classification rests on a single empirical study. Its boundaries were derived from a corpus rather than from prior theory, by grouping comments by normalised text, inspecting the most frequent forms and expanding patterns iteratively. Validation on 800 manually re-labelled comments gave the three-class scheme 96.5% overall accuracy, with agent steering at 94.5% precision and 95.0% recall; the authors report that residual misclassification falls mainly between agent steering and direct human review, reflecting lexical overlap between imperative forms and informal discourse.

## Related Terms

- [[DefinedTerm/agentic-code-review]]
- [[DefinedTerm/code-review-agent]]
- [[DefinedTerm/review-bottleneck]]
