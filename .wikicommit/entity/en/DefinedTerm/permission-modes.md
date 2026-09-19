---
title: "Permission Modes"
type: "schema:DefinedTerm"
lang: en
tags: [agent-safety, human-oversight, agent-tooling]
sources:
  - type: url
    url: 'https://docs.claude.com/en/api/agent-sdk/permissions'
    hash: sha256:c4534377b28cb19c1b4d96673f98b2d47028ae3535bb6eda233c73d3933d9f61
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A session-wide setting that determines an agent's baseline handling of tool requests matching no explicit rule — from denying everything that would prompt, through auto-accepting file edits, to bypassing checks. It sets the default, not the ceiling: deny and ask rules are documented as applying regardless of the mode."
---

A permission mode is a session-wide setting that provides global control over how an agent uses
tools. In the [[SoftwareApplication/claude-agent-sdk]] documentation it occupies a specific position
in a fixed evaluation order — after hooks, deny rules and ask rules have been consulted, and before
allow rules and the runtime callback — which is what gives the concept its precise meaning: the mode
decides the baseline treatment of a request that earlier steps did not resolve.

That position is the substance of the idea. Because deny and ask rules are evaluated before the mode
applies, the documentation states that both continue to take effect even in the most permissive
mode, so a mode raises or lowers the default without removing the controls declared around it.

## Usage

Six modes are documented. `default` adds no mode-based auto-approvals, so a call needing approval and
matching no allow rule reaches the callback. `dontAsk` denies anything that would otherwise prompt
and never invokes the callback at all, while still running calls approved by rules and calls that
need no approval. `acceptEdits` auto-approves file edits and filesystem operations, leaving other
tools to normal handling. `bypassPermissions` runs tools without prompting, apart from a documented
set of actions no mode auto-approves. `plan` keeps file edits from being auto-approved so that the
agent explores and plans without editing source files. `auto` delegates the decision to a model
classifier.

A mode can be set when a query is created or changed during a session, which the documentation
suggests using to start restrictive and loosen as trust builds. For subagents it is inherited from
the parent session, with the documented exception that the most permissive mode is never applied to
a subagent unless the parent itself runs in it — the stated reason being that subagents may have
different system prompts and less constrained behavior, so inheriting it would grant them full
autonomous system access.

## When It Applies

The concept applies to harnesses where tool permissions are evaluated outside the model, and it
assumes a rule system alongside it — a mode alone expresses only a posture, not a policy. The
documentation illustrates the distinction with a locked-down configuration that pairs an explicit
allow list with `dontAsk`, so that listed tools run and every other prompting call is denied.

Its documented misuse is treating a mode as a constraint rather than a default: an allow list does
not narrow `bypassPermissions`, because unlisted tools match no allow rule and are approved by the
mode itself. To put a tool out of reach the documentation directs the reader to a deny rule instead.

How well-established it is: this is one vendor's documented design for its own SDK, and the mode
names above are that SDK's vocabulary rather than an industry-wide standard.

## Related Terms

- [[SoftwareApplication/claude-agent-sdk]] — the SDK whose documentation defines these modes
- [[DefinedTerm/deny-first-permission-evaluation]] — the safety posture the ordering expresses
- [[DefinedTerm/human-in-the-loop]] — what the prompting modes fall back on
- [[DefinedTerm/agent-hooks]] — the step evaluated before the mode, able to deny in any mode
- [[DefinedTerm/approval-fatigue]] — the human cost these modes trade against
