---
title: "Orchestration Tax"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/own-the-outer-loop/'
    hash: sha256:4945c6720401f08dd3c43a7ec8fd0b79a1c8eb6f08bfa4b0da49f6e4a0c6173a
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "As framed in Addy Osmani's 'Own the Outer Loop' keynote, the cognitive cost of directing and reviewing multiple parallel coding agents — steering them away from bad behavior, triaging their output, and verifying key assumptions before letting them run — which does not scale down just because spinning up more agents has become easy."
---

In his "Own the Outer Loop" keynote, Addy Osmani frames the orchestration tax as the cognitive cost of directing and reviewing multiple coding agents running in parallel. Spinning up more agents has become easy, but a person's own cognitive bandwidth does not parallelize the same way: steering an agent away from its worst behaviors, sorting through the work it produces to find what needs attention, directing it toward what matters most, and verifying important constraints and dangerous assumptions before letting it run are all described as work that cannot be automated away.

## Usage

The source states the tax is worse on brownfield systems, because the behavior that needs auditing doesn't live in the code — it lives in "the scars," in the source's own words. Four mitigations are named: prioritizing attention in architectural decisions, using worktrees, scopes, and evidence to reduce coupling between an initial plan and the work that emerges from it, time-boxing the effort spent resolving unactionable steps, and making changes to the software strictly opt-in. It is presented as one of three hidden costs of agentic delegation, alongside cognitive surrender and cognitive debt.

## Related Terms

[[DefinedTerm/outer-loop]], [[DefinedTerm/cognitive-surrender]], [[DefinedTerm/cognitive-debt]]
