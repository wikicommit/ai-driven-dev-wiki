---
title: "Spec-driven development with AI: Get started with a new open source toolkit"
type: "schema:BlogPosting"
lang: en
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/'
    hash: sha256:c69d76f7139da5ec34ed3ad1c5ad12521c158fa6e73d753fdcf990baaa6cba75
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"
tags: [spec-driven-development, agents, coding-tools, legacy-modernization]

properties:
  description: "GitHub's announcement of Spec Kit, an open-source spec-driven development toolkit, setting out its four-phase process and the argument that intent, not code, should be the source of truth."
  author: ["Den Delimarsky"]
  datePublished: "2025-09-02"
  publisher: "[[Organization/github]]"
---

GitHub's announcement of [[SoftwareApplication/github-spec-kit]], an open-source toolkit for
[[DefinedTerm/spec-driven-development]]. The post opens from a pattern the author says has
emerged as coding agents grew more powerful: you describe a goal, get code back, and it often
looks right without quite working — an approach it calls "vibe-coding", good for quick
prototypes and less reliable for mission-critical applications or existing codebases.

Its diagnosis is that the problem is not the agent's coding ability but the approach: that
developers treat coding agents like search engines when they should be treated more like
literal-minded pair programmers, excellent at pattern recognition but still needing
unambiguous instructions. The proposed answer is to rethink specifications as living,
executable artifacts that evolve with the project and serve as the shared source of truth.

## Key Points

- The post defines spec-driven development as starting with a spec rather than coding first
  and documenting later — a contract for how the code should behave, which becomes the source
  of truth tools and agents use to generate, test and validate code.
- Spec Kit's process runs in four phases with checkpoints, and the author states you do not
  move to the next phase until the current task is fully validated. **Specify**: a high-level
  description of what you are building and why, from which the agent generates a detailed
  specification about user journeys and outcomes rather than technical stacks. **Plan**: you
  supply stack, architecture and constraints and the agent produces a technical plan, with
  the option to ask for multiple variations to compare. **Tasks**: the agent breaks spec and
  plan into small reviewable chunks each implementable and testable in isolation. **Implement**:
  the agent works through tasks while the developer reviews focused changes rather than
  thousand-line code dumps.
- The author stresses that the developer's role is not only to steer but to verify: the
  process builds in explicit checkpoints to critique what was generated, spot gaps and course
  correct — the AI generates the artifacts, the developer ensures they are right.
- Spec Kit works with coding agents including GitHub Copilot, Claude Code and Gemini CLI, and
  is set up by installing the `specify` command-line tool, then driven with `/specify`,
  `/plan` and `/tasks` commands.
- The stated reason the approach works is that language models are exceptional at pattern
  completion but not at mind reading: a vague prompt forces the model to guess at potentially
  thousands of unstated requirements, and some guesses will be wrong in ways not discovered
  until deep into implementation.
- For larger organizations the post argues the spec and plan give security policies,
  compliance rules, design system constraints and integration needs a home the AI can
  actually use, instead of living in someone's head, an unread wiki, or scattered Slack
  conversations.
- Three scenarios are named where the approach works especially well: greenfield
  (zero-to-one) projects; feature work in existing systems (N-to-N+1), which the post calls
  the most powerful case because a spec forces clarity on how the feature interacts with what
  exists; and legacy modernization, where the original intent is often lost and can be
  recaptured as a modern spec before rebuilding.
- The post states the core benefit as separating the stable "what" from the flexible "how",
  enabling iterative development without expensive rewrites, and frames the wider shift as
  moving from "code is the source of truth" to "intent is the source of truth" — which it
  attributes not to documentation mattering more but to AI making specifications executable.
- GitHub says it open sourced the toolkit because the approach is bigger than any one tool or
  company, calling the real innovation the process rather than the tool, and describes Spec
  Kit as its experiment in making that transition real.

## Context

This is a first-party announcement of GitHub's own toolkit on GitHub's own blog, and its
claims for the approach rest on the author's stated reasoning about how language models
behave rather than on any evaluation, benchmark or user study. The post itself describes Spec
Kit as an experiment and closes by asking readers what to improve, which is a fair
characterization of how settled the approach was at publication.

The post's "vibe-coding" framing is the contrast term for the practice it advocates — see
[[DefinedTerm/vibe-coding]] — and its four-phase, human-gated structure is one concrete
implementation among several that [[DefinedTerm/spec-driven-development]] covers. Its remark
that advanced context engineering practices may be needed for feature work in existing
systems points at [[DefinedTerm/context-engineering]].
