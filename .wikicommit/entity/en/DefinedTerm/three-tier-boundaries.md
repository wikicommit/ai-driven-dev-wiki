---
title: "Three-Tier Boundaries"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/good-spec/'
    hash: sha256:fbb1e0c078b1d920689cbc3c652ad4bf253d5b39c77f957cab7ee4e6cd1ff5fa
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A pattern for specifying an AI coding agent's boundaries as three tiers — Always do, Ask first, Never do — rather than a flat list of rules, found by a GitHub analysis of agent configuration files to be more effective than an undifferentiated list of don'ts."
---

Three-tier boundaries is a pattern for writing the constraints in an AI coding agent's specification as three distinct tiers rather than a flat list of rules: **Always do** — actions the agent takes without asking, such as running tests before commits; **Ask first** — actions needing human approval, such as modifying a database schema or adding a dependency; and **Never do** — hard stops, such as committing secrets or editing vendored directories.

## Usage

The pattern is reported to come from a GitHub analysis of over 2,500 agent configuration files, which found it more effective than a simple list of prohibitions because it lets an agent proceed confidently on "Always" items, flag "Ask first" items for review, and hard-stop on "Never" items, rather than treating every rule as carrying the same weight. "Never commit secrets" is reported as the single most common helpful constraint found in that study.

## When It Applies

It applies wherever a specification needs to give an agent enough autonomy to act without constant supervision while still gating actions that carry real risk, such as changing CI/CD configuration or database schemas. The source frames it as more nuanced than a flat list of rules precisely because it distinguishes actions that are always safe from ones that need oversight and ones that are categorically off-limits.

## Related Terms

[[BlogPosting/good-spec]]
