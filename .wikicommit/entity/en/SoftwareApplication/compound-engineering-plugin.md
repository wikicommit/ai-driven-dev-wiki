---
title: "Compound Engineering Plugin"
type: "schema:SoftwareApplication"
lang: en
tags: [claude-code-plugin, multi-agent, code-review]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/claude-code-agent-teams/'
    hash: sha256:b36f513e61d7ef1ac90ab862218ac5db53654893d583aba69626a3e5ac82e049
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Claude Code plugin from Every that adds specialized review agents and a plan → work → review → compound cycle, built on the idea that each unit of engineering work should make subsequent units easier."
  applicationCategory: "Claude Code plugin"
  author: "Every"
---

The Compound Engineering Plugin is a [[SoftwareApplication/claude-code]] plugin from Every. It adds specialized review agents and a plan → work → review → compound cycle designed around the idea that each unit of engineering work should make subsequent units easier. It is installed from inside Claude Code by adding its GitHub repository as a plugin marketplace and then installing `compound-engineering`.

## Capabilities

- `/workflows:plan` turns feature ideas into detailed implementation plans.
- `/workflows:review` runs multi-agent code review before merging, with a specialized reviewer each for security, performance, architecture and complexity.
- `/workflows:compound` documents learnings so that future agents benefit from past work.

## Adoption & Ecosystem

In [[BlogPosting/claude-code-swarms]], Addy Osmani suggests it for anyone wanting a more structured workflow around [[DefinedTerm/agent-teams]]. He describes the plugin's philosophy as 80% planning and review and 20% execution, and argues that this maps onto what makes agent teams effective: the better the specs, the better the agent output, and the more learnings are codified, the less each subsequent agent flails. The same post states that the plugin also works with [[SoftwareApplication/opencode]] and, experimentally, with Codex.
