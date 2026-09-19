---
title: "Agentic Ghosting"
type: "schema:DefinedTerm"
lang: en
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/generative-ai/agent-pull-requests-are-everywhere-heres-how-to-review-them/'
    hash: sha256:0b1fe0a68eef47c6de5a67a1c9483c7cb93a8e4e6377a7517e85bc1a71bd2a61
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"
tags: [agents, code-review, human-oversight]

properties:
  description: "GitHub's name, in its guide to reviewing agent pull requests, for an agent-authored pull request going silent, or circling without addressing the point, after a reviewer has invested a thorough review."
---

Agentic ghosting is the pattern in which a reviewer leaves a thorough review on an
agent-generated pull request — explaining the issue, providing context, suggesting a
direction — and the pull request then goes quiet, or the agent responds in a way that
misses the point entirely and runs in circles. GitHub's guide to reviewing agent pull
requests names it as one of five red flags, and frames its cost as review time sunk into
something that goes nowhere: another round invested, still nothing useful. The phrase is
that post's own label rather than a term it presents as established.

## Usage

In that guide the term is deployed when triaging which agent pull requests are worth deep
review. GitHub's guide states that larger pull requests with no structured plan correlate strongly with
agent abandonment or misalignment — the larger and less scoped the pull request, the more
likely the review effort is wasted. Its advice is therefore to check, before investing,
whether the pull request has been responsive in previous rounds and whether it has a clear
implementation plan or the agent simply started writing code.

Where no plan exists, the guide advises requesting a breakdown before writing a single
review comment, and supplies wording for it — asking the author to break the change into
smaller scoped units or to summarize what each part does and why it is structured that way.
It characterizes that response as firm, short and not personal, and as saving the reviewer
an hour. The guide separately gives four conditions for sending a pull request back to be
made smaller — among them a diff touching more than five
unrelated files, and the agent having no implementation plan or an empty pull request body.

## Related Terms

- [[DefinedTerm/ci-gaming]] — another failure mode named in the same guide
- [[DefinedTerm/review-bottleneck]] — the scarcity of review capacity this pattern consumes
- [[DefinedTerm/developer-agent-misalignment]] — a related category, scoped there to cases where the developer visibly pushes back
- [[DefinedTerm/human-in-the-loop]] — the broader set of arrangements for keeping a person involved, of which review is one
