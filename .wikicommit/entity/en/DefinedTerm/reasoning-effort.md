---
title: "Reasoning Effort"
type: "schema:DefinedTerm"
lang: en
tags: [llm, coding-tools, claude-code, cost]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/april-23-postmortem'
    hash: sha256:269dd6e147333715b02167db5eedbc394fe254ceebed15d9cf7f2a05a25c87f5
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A user-facing setting that selects how long a model thinks before answering, trading output quality against latency and token consumption. In the one implementation this page documents, the named levels correspond to chosen points along the test-time-compute curve and the selected one is sent to the API as a parameter."
---

Reasoning effort is a setting that trades how long a model thinks against latency and token
consumption. [[BlogPosting/update-on-recent-claude-code-quality-reports]] describes how it is
constructed in [[SoftwareApplication/claude-code]]: effort levels are calibrated per model as
chosen points along the test-time-compute curve, the product layer picks one of those points as its
default and sends it to the Messages API as an effort parameter, and the remaining points are
offered to the user through a command. The general relationship Anthropic states is that the longer
the model thinks, the better the output.

## Usage

The setting exists because the tradeoff has two sides that are both real to users. That post
reports that when Opus 4.6 shipped in Claude Code with effort defaulting to `high`, users found
that it would occasionally think for so long the interface appeared frozen, with what Anthropic
describes as disproportionate latency and token usage for those users. Lowering the default to `medium` was measured internally as
slightly lower intelligence for significantly less latency on most tasks, without the occasional
very long thinking tails, and as making users' usage limits go further.

Anthropic lowered the default to `medium` on March 4, 2026, a change it states affected Sonnet 4.6
as well as Opus 4.6. What followed is the part of the account with the wider lesson. Users reported
that Claude Code felt less intelligent, and Anthropic reversed the decision on April 7, saying users had told them
they would rather default to higher intelligence and opt down for simple tasks; the defaults after
that reversal are stated as `xhigh` for Opus 4.7 and `high` for every other model. Anthropic
records having first tried to solve the problem through visibility rather than through the default
— startup notices, an inline effort selector, and reinstating ultrathink — and reports that most
users stayed on the medium default regardless.

## When It Applies

The setting applies wherever the same model can usefully be run at different amounts of thinking,
and it assumes a harness that exposes the choice and a model whose effort levels have been
calibrated. Anthropic's own conclusion about where to set it is blunt — lowering
the default was the wrong tradeoff — and its stated reading of user feedback is that people would
rather default to higher intelligence and opt into lower effort for simple tasks.

Two limits on this account are worth keeping in view. It comes from one vendor writing about its
own product, and the measurements behind both the original change and its reversal are internal
evaluations and user feedback rather than anything independently reported. The episode it describes
is also specifically a defaults problem — every effort level remained reachable throughout — and
what it records on that point is narrow: most Claude Code users stayed on the medium default even
after notices, a selector and the return of ultrathink told them they could change it.

## Related Terms

[[DefinedTerm/token-caching]], [[DefinedTerm/agent-harness]], [[DefinedTerm/context-engineering]]
