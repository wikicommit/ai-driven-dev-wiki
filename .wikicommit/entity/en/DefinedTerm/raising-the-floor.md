---
title: "Raising the Floor"
type: "schema:DefinedTerm"
lang: en
tags: [team-practices, coding-tools, claude-code]
sources:
  - type: url
    url: 'https://toss.tech/article/harness-for-team-productivity'
    hash: sha256:c578d09dce25f7293277154d1741cd800ad5d6afd7700ee897468e966f53f939
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "One engineer's name for treating the variation in what colleagues get out of the same model as an organizational problem to be closed at the team's weakest point, rather than as an individual skill each person should improve, by packaging the team's best working methods so that anyone can invoke them."
---

Raising the Floor is the name [[BlogPosting/raising-productivity-floor-with-harness]] gives to
raising the floor of a team's productivity with a language model — levelling the whole team up, in
that post's phrasing, by working on its weakest case.
The premise is that a gap in know-how about controlling the tool exists within a team independently
of coding ability, and that closing it is an organizational task: the post's framing is that leaving
the gap to individual aptitude is a loss the organization bears.

The post's illustration of the gap is two engineers given the same task in the same repository. One
sets up context first — supplying the repository's coding guidelines, lint rules and existing code
patterns before asking for anything — and has a change that fits the team's conventions in ten
minutes. The other opens with a bare request, receives code in a generic style, and spends an hour
in a correction loop. The author names the difference as whether context was designed before the
work started.

## Usage

The mechanism the post proposes is distribution. Its worked example is a single slash command that
carries the whole of a strong engineer's workflow — collecting the context of the feature through
conversation, opening a tracking issue, creating a branch, writing an implementation plan for a
human to review and approve, implementing, and opening a pull request for review — so that an
engineer who would not have assembled that sequence runs it at the same quality by invoking one
command. The same idea is applied to team discipline: a hook that intercepts a commit attempt on
the main branch and redirects the agent to create a feature branch instead, which the author
contrasts with a linter that only reports an error and blocks.

Generic open-source plugin collections are treated as a legitimate starting point for this — the
post compares them to what `oh-my-zsh` did for terminal productivity — but not as sufficient,
because an externally defined general-purpose tool does not know a team's domain, and each team has
its own boundary between what a model can be left to do and what a person must approve.

## When It Applies

The term applies where the variation being addressed is in method rather than in capability, and it
assumes the good method can actually be written down and invoked — the post's whole argument is
that know-how should move from individual sense into a system a team designs and distributes. It
assumes, too, a tool that supports that distribution; the post is written around one agent's plugin
and marketplace mechanism.

How well established it is: this is one engineer's argument in a single post, offered as a
direction rather than a measured outcome. The author describes the piece as closer to a direction
than to a concrete success story, and several readers in its comment thread take it to task for
staying abstract.

## Related Terms

[[DefinedTerm/executable-ssot]], [[DefinedTerm/claude-code-plugin-marketplace]],
[[DefinedTerm/agent-harness]], [[DefinedTerm/software-3-0]]
