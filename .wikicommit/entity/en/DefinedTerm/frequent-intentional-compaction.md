---
title: "Frequent Intentional Compaction"
type: "schema:DefinedTerm"
lang: en
tags: [context-engineering, coding-agents]
sources:
  - type: url
    url: 'https://www.humanlayer.dev/blog/advanced-context-engineering'
    hash: sha256:b5755938c78f425250aee7de4d4a3136d208b1d531e6999969cd3e9af536d9a1
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A family of techniques, named by HumanLayer, for working with coding agents by designing the whole development workflow around context management — keeping context utilization around 40-60% and splitting work into research, plan and implement steps with human review in between."
---

Frequent intentional compaction is the name HumanLayer's [[BlogPosting/advanced-context-engineering-for-coding-agents]]
gives to a family of techniques for getting coding agents to work in large, complex codebases: designing
the entire development workflow around context management, deliberately structuring how context is fed
to the agent throughout, and keeping context utilization in roughly the 40%-60% range depending on the
complexity of the problem. It extends what the post calls "intentional compaction" — pausing as the
context fills, writing the goal, approach, progress and current failure to a file, and starting over
with a fresh context window — from an occasional rescue into the structure of every task.

## Usage

In the post, the team practises it as a three-step ("ish") workflow for each feature or bug. **Research**
builds an understanding of the relevant files, how information flows and possible causes of a problem;
**plan** sets out the exact steps, the files to edit and how, and the testing and verification for each
phase; **implement** steps through the plan phase by phase, often compacting the current status back into
the plan file after each verified phase. The author notes they sometimes skip research or run several
passes of it, uses subagents for the searching and summarizing so the parent context stays clean, and
says only the implementation step needs a git worktree. The post publishes the team's research,
planning and implementation prompts.

## When It Applies

The post presents it for brownfield codebases and complex problems, where it reports that naive
chat-style use tends to fail. It assumes a human who stays deeply engaged: the author stresses that it is
"not magic", that frequent intentional compaction makes performance better but what makes it good enough
for hard problems is building high-leverage human review into the pipeline — reviewing research and plans
rather than only code, because an error in research or a plan multiplies into many bad lines of code. It
fails when that review does not catch shallow research: the post reports an attempt to remove Hadoop
dependencies from parquet-java that did not go well because the research did not go deep enough, and
suggests at least one codebase expert is probably needed. The evidence is the author's team's own
experience (a bug fix and 35k lines of features in the BAML Rust codebase, an intern shipping 2 PRs on
his first day and 10 on his 8th); the author himself says he does not believe research/plan/implement is the right approach
for most teams, while arguing every team needs a process that keeps members aligned and helps them learn
unfamiliar code quickly.

## Related Terms

- [[DefinedTerm/compaction]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/sub-agent-architecture]]
- [[DefinedTerm/context-rot]]
