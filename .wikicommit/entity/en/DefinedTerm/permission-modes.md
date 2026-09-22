---
title: "Permission Modes"
type: "schema:DefinedTerm"
lang: en
tags: [agent-safety, human-oversight, agent-tooling, prompt-injection]
sources:
  - type: url
    url: 'https://docs.claude.com/en/api/agent-sdk/permissions'
    hash: sha256:c4534377b28cb19c1b4d96673f98b2d47028ae3535bb6eda233c73d3933d9f61
  - type: url
    url: 'https://www.anthropic.com/engineering/claude-code-best-practices'
    hash: sha256:9aae24f8b850a5f9c8a6f561be1fecf54f29e1ddc4658d00ecded22bccb82b82
  - type: url
    url: 'https://simonwillison.net/2026/Jul/21/cat-and-thariq/'
    hash: sha256:a27deba3b2ae555c7354fa9733173cb7efc80237fc406cc7f265170dc8a99b5b
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

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

Where the SDK documentation presents the modes as a list of equal options, the Claude Code
best-practices documentation describes which one a session actually starts in, and treats that as a
plan-dependent default rather than a user choice. On Pro, Max and Team plans, **auto mode** is the
built-in starting mode for interactive terminal and VS Code sessions; on other plans it is **Manual
mode**. The two are characterised by who does the reviewing. In Manual mode the agent asks before
anything that might modify the system — file writes, Bash commands, MCP tools — which the
documentation itself calls safe but tedious, observing that by the tenth approval a user is clicking
through rather than reviewing (compare [[DefinedTerm/approval-fatigue]]). In auto mode a separate
classifier model reviews most actions instead of the user and blocks only what looks risky, with
three categories named: scope escalation, unknown infrastructure, and hostile-content-driven actions.

Two tools are documented as cutting the interruptions in Manual mode while applying in auto mode as
well: permission allowlists, pre-approving specific tools known to be safe, and
[[DefinedTerm/sandboxing]], enabling OS-level isolation of filesystem and network so the agent can
work more freely within defined boundaries. The same documentation notes a behavioural difference
between interactive and non-interactive use of the classifier mode: when it repeatedly blocks actions
in a non-interactive run, the run is not stopped, and a documented fallback applies instead.

### How the classifier mode works, as its makers describe it

Two members of the Claude Code team gave a fuller mental model of auto mode in conversation, relayed
in [[BlogPosting/a-fireside-chat-with-cat-and-thariq-from-the-claude-code-team]]. On their account
the classifier is a Sonnet model, and what it judges is not the tool call alone but the call
*together with* the context of the conversation — the user's own instruction included. That is what
they present as the mode's distinctive property: permissions that depend on the request. Their
illustration is that one would not grant a coding agent standing permission to push to a remote, but
that saying "push this to GitHub" should permit it and saying "don't push" should cause it to be
denied — and they report the second case arising often in practice, where the agent proposes
something helpful and the mode surfaces it because the user had ruled it out.

They also describe it as complementing rather than duplicating OS-level isolation. Sandboxing, on
their account, has so many edge cases that following them deterministically is hard; so when
something needs to escape the sandbox — a network request is the example given — the classifier can
inspect that request and judge whether it makes sense before allowing it. More generally, one of
them states that the mode interacts with any permission prompt the user would otherwise have seen.
Two adjacent mechanisms are mentioned in the same discussion: trusted devices for users of remote
control, and credential injection, in which a proxy inserts credentials into the agent's outbound
requests so that they are usable by the agent without being accessible to it.

## When It Applies

The concept applies to harnesses where tool permissions are evaluated outside the model, and it
assumes a rule system alongside it — a mode alone expresses only a posture, not a policy. The
documentation illustrates the distinction with a locked-down configuration that pairs an explicit
allow list with `dontAsk`, so that listed tools run and every other prompting call is denied.

Its documented misuse is treating a mode as a constraint rather than a default: an allow list does
not narrow `bypassPermissions`, because unlisted tools match no allow rule and are approved by the
mode itself. To put a tool out of reach the documentation directs the reader to a deny rule instead.

How well-established it is: this is one vendor's documented design for its own SDK and its own coding
tool, and the mode names above are that vendor's vocabulary rather than an industry-wide standard.
The second source adds a further caveat of its own kind — which mode a session starts in there is
tied to the user's subscription plan, so the starting posture is a commercial decision as much as a
safety one.

The strongest claims made for the classifier mode are the vendor's own, made by its team in the
conversation cited above rather than in documentation, and the interviewer challenged one of them on
the spot. They report almost everyone inside the company using auto mode and call it the best way to
do long-running work in Claude Code safely; they cite thousands of evals, evals run across every
internal user, and multiple commissioned red teams building adversarial environments with prompt
injections and malicious inputs, stating that every issue those teams found has been mitigated. They
decline the stronger version explicitly — it does not catch 100% of things, which they say would be
far too strong a claim — and pitch the comparison instead as relative: for the risk categories they
care about, notably [[DefinedTerm/prompt-injection]] and data exfiltration, they claim the risk is
far lower than that of the average human reviewer. They said the supporting evals would be published,
and none had been at the time that conversation was relayed, so the basis for these figures is not
independently checkable from here. One further detail of provenance: they date internal
use to January, well before it reached the public, and they give this mode as the foundation that makes their Slack-resident agent
[[SoftwareApplication/claude-tag]] viable at all, since an agent reading a channel anyone can post
into is exposed to prompt injection by construction.

## Related Terms

- [[SoftwareApplication/claude-agent-sdk]] — the SDK whose documentation defines these modes
- [[DefinedTerm/deny-first-permission-evaluation]] — the safety posture the ordering expresses
- [[DefinedTerm/human-in-the-loop]] — what the prompting modes fall back on
- [[DefinedTerm/agent-hooks]] — the step evaluated before the mode, able to deny in any mode
- [[DefinedTerm/approval-fatigue]] — the human cost these modes trade against
