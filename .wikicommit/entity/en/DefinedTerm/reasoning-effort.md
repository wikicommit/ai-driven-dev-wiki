---
title: "Reasoning Effort"
type: "schema:DefinedTerm"
lang: en
tags: [llm, coding-tools, claude-code, cost]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/april-23-postmortem'
    hash: sha256:269dd6e147333715b02167db5eedbc394fe254ceebed15d9cf7f2a05a25c87f5
  - type: url
    url: 'https://developers.googleblog.com/new-gemini-api-updates-for-gemini-3/'
    hash: sha256:5c0c9a076fa04762c9220c98f1a90a42776dffeff714891ebb38383da16fa94f
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A setting that selects how long or how deeply a model thinks before answering, trading output quality against latency and token consumption. The implementations this page documents expose it as a small set of named levels sent to the model API as a parameter."
---

Reasoning effort is a setting that trades how long or how deeply a model thinks against latency and
token consumption. Two vendors' implementations are documented here, each exposing it as named levels
passed to its model API: Anthropic's effort parameter as used in [[SoftwareApplication/claude-code]],
and the `thinking_level` parameter of Google's [[SoftwareApplication/gemini-api]].

## Usage

### Anthropic: effort levels in Claude Code

[[BlogPosting/update-on-recent-claude-code-quality-reports]] describes how the setting is constructed
in Claude Code: effort levels are calibrated per model as chosen points along the test-time-compute
curve, the product layer picks one of those points as its default and sends it to the Messages API as
an effort parameter, and the remaining points are offered to the user through a command. The general
relationship Anthropic states is that the longer the model thinks, the better the output.

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

### Google: `thinking_level` in the Gemini API

[[BlogPosting/new-gemini-api-updates-for-gemini-3]] introduces `thinking_level`, a parameter from
Gemini 3 onwards that controls the maximum depth of the model's thinking process before it produces a
response. Google states that Gemini 3 treats the levels as relative guidelines for reasoning rather
than strict token guarantees. It suggests "high" for complex tasks that require optimal thinking — its
examples are strategic business analysis and scanning code for vulnerabilities — and "low" for
latency- and cost-sensitive applications such as structured data extraction and summarization.

## When It Applies

The setting applies wherever the same model can usefully be run at different amounts of thinking,
and it assumes a harness that exposes the choice and a model whose effort levels have been
calibrated. Google's guidance for `thinking_level` frames the choice by task: a high level for complex
analysis, a low one where latency and cost matter more. Anthropic's own conclusion about where to set
its default is blunt — lowering the default was the wrong tradeoff — and its stated reading of user feedback is that people would
rather default to higher intelligence and opt into lower effort for simple tasks.

Two limits on these accounts are worth keeping in view. Each comes from a vendor writing about its
own product: Google's describes the parameter and when to use each level without reporting
measurements, and the measurements behind both Anthropic's original change and its reversal are
internal evaluations and user feedback rather than anything independently reported. The Anthropic
episode is also specifically a defaults problem — every effort level remained reachable throughout — and
what it records on that point is narrow: most Claude Code users stayed on the medium default even
after notices, a selector and the return of ultrathink told them they could change it.

## Related Terms

[[DefinedTerm/token-caching]], [[DefinedTerm/agent-harness]], [[DefinedTerm/context-engineering]],
[[DefinedTerm/thought-signature]]
