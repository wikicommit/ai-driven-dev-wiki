---
title: "AI IDE"
type: "schema:DefinedTerm"
lang: en
tags: [agents, coding-tools]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.12231'
    hash: sha256:08aa95b018a1374f9de491d626d4f394b8efec41d830ef1726a1b8db6a69d9d6
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An integrated development environment built with artificial intelligence as a core architectural component rather than as a plugin layered onto an existing editor, giving the model deeper access to project-wide context, internal editor state and interaction history."
---

An AI IDE is an integrated development environment in which AI is a core architectural component rather
than an optional extension. The distinction
[[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] draws is against the plugin arrangement —
VS Code with a [[SoftwareApplication/github-copilot]] extension, for instance — where the assistant
operates within the constraints the host editor imposes, limiting its access to runtime state, internal
editor signals and fine-grained interaction data. In an AI IDE the model is integrated into the core
editor infrastructure instead, which that study argues is what enables capabilities beyond code
completion: autonomous task decomposition, multi-file refactoring, architectural reasoning,
context-aware generation, and continuous alignment with project-specific configuration.

## Usage

The category as that study uses it is defined partly by a shared feature: the tools it examines all let
developers define [[DefinedTerm/ai-ide-rules]] that the IDE must follow during code generation and chat.
The five it studies on that basis are [[SoftwareApplication/cursor]],
[[SoftwareApplication/windsurf]], [[SoftwareApplication/trae]], [[SoftwareApplication/qoder]] and
[[SoftwareApplication/kiro]].

That study's mining of 83 projects declared as built with an AI IDE gives a picture of where the
category was being used at the time. TypeScript dominates the codebases at 50.6%, followed by Python at
14.4% and JavaScript at 9.6%; web application development accounts for the majority of domains, with
full-stack, frontend and backend projects together making up 56.6%. The projects are small: over half
have fewer than 50 commits, and solo developers or teams of two to three account for the large majority.
The study reports that many of them were created between June 2025 and September 2025.

The survey side gives a different view of the same question, since respondents report on their own
practice rather than on a filtered project set. Among 99 practitioners, Cursor was the most widely
adopted at 57, closely followed by the VS Code plus Copilot setup at 51 — that is, a plugin arrangement
rather than an AI IDE — with Kiro at 37, Trae at 24, Windsurf at 23 and Qoder at 16. A further 34
reported using Antigravity, and Claude Code, Codex and OpenCode were named under an "Other" option.

## When It Applies

The term is useful where the architectural distinction it names actually makes a difference — that is,
where the depth of the model's access to editor state and project context is the thing under
discussion. Where it is not, "AI coding tool" covers the same ground with fewer commitments; the survey
data above is the clearest illustration, since a plugin setup sits second in adoption among developers
who also use AI IDEs, and the study counts it separately without treating it as one.

The study offers no operational test for membership beyond the architectural characterisation and its
own selection of five tools that support user-defined rules, so where a given tool falls is left to
judgement. It does note that the ecosystem is evolving rapidly — both the underlying foundation models
and the rule-injection mechanisms undergo frequent updates — and presents its own findings as a
snapshot of current context-engineering practices.

## Related Terms

- [[DefinedTerm/ai-ide-rules]] — the configuration mechanism these tools share
- [[ScholarlyArticle/rule-taxonomy-and-evolution-in-ai-ides]] — the study this account is drawn from
- [[DefinedTerm/ai-coding-agent]] — the agent-shaped sibling of this category
- [[DefinedTerm/agentic-coding]] — the practice these tools are built for
