---
title: "60 million Copilot code reviews and counting"
type: "schema:BlogPosting"
lang: en
tags: [code-review, agents, coding-tools]
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/60-million-copilot-code-reviews-and-counting/'
    hash: sha256:0fb7098fdd6a821dd84f639e8def29c0543822c62545b031dd7e3d62fdf5b5e2
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A GitHub blog post on how Copilot code review changed after its launch: a redefinition of a good review around accuracy, signal and speed, a move to an agentic architecture that retrieves repository context, and interface changes meant to make reviews easier to act on."
  author: ["Ria Gopu", "David Apirian"]
  datePublished: "2026-03-05"
  publisher: "[[Organization/github]]"
---

A post on GitHub's blog, published on March 5, 2026 by a GitHub product manager and a senior director of software engineering, describing how [[SoftwareApplication/github-copilot-code-review]] has changed since its initial launch the previous April. Its framing is that AI is accelerating the pace of code changes, and that teams need help reviewing and trusting code at that scale; it reports that usage of the feature has grown tenfold since launch and now accounts for more than one in five code reviews on GitHub.

Most of the post explains how GitHub's own definition of a "good" code review shifted. When the team started building the feature in 2024, the stated goal was thoroughness; the post says what developers actually value turned out to be high-signal feedback that moves a pull request forward quickly, and that the team now tunes the agent through a continuous evaluation loop against three qualities — accuracy, signal and speed. It then describes the redesigned [[DefinedTerm/agentic-code-review]] architecture behind the feature and a set of changes to how feedback is presented in the pull request.

## Key Points

- Accuracy is evaluated in two ways: internal testing against known code issues, and production signals from real pull requests — thumbs-up and thumbs-down reactions on comments, and whether flagged issues are resolved before merging.
- On signal, the post argues that more comments do not make a better review: in 71% of reviews Copilot code review surfaces actionable feedback, and in the remaining 29% it says nothing at all ("Silence is better than noise"). It reports averaging about 5.1 comments per review.
- On speed, GitHub describes a deliberate trade-off in favour of signal: in one change, adopting a more advanced reasoning model raised positive feedback rates by 6% while increasing review latency by 16%, which the post calls the right exchange.
- The redeveloped agentic design retrieves context and explores the repository to understand logic, architecture and invariants; the post attributes an initial 8.1% increase in positive feedback to this shift alone.
- The post lists four reasons for that gain: the agent records issues as it reads rather than only at the end (which previously led to "forgetting" early discoveries), it can keep memory across reviews, it can plan its review strategy ahead of time for long pull requests, and it reads linked issues and pull requests to catch code that looks reasonable in isolation but does not match the project's requirements.
- Presentation changes described are multi-line comments attached to logical code ranges instead of single lines, clustering repeated instances of the same pattern error into one comment, and batch autofixes that apply a whole class of suggested fixes at once.
- The post states that more than 12,000 organizations run Copilot code review automatically on every pull request, and quotes a customer story from WEX, which made it a default across every repository — backing that comes from GitHub's own customer material.
- Stated next steps are deeper personalization — learning a team's unwritten preferences — and two-way conversations that let developers refine fixes and explore alternatives before merging.

## Context

This is a vendor's account of its own product, and every figure in it — the share of reviews, the feedback-rate changes, the organization count — is GitHub's own measurement, and the post cites no outside source for any of them. For the feature's configuration, effort levels and customization surfaces, see [[SoftwareApplication/github-copilot-code-review]].
