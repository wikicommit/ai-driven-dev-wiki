---
title: "Evolving Spec-Driven Development: Conductor Now Supports Antigravity"
type: "schema:BlogPosting"
lang: en
tags: [spec-driven-development, coding-tools, agent-tooling]
sources:
  - type: url
    url: 'https://developers.googleblog.com/evolving-spec-driven-development-conductor-now-supports-antigravity/'
    hash: sha256:98f164a5f001fb955c64f15d7e50993bc6a3d3bf8125709253448759591049a7
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Google's announcement that Conductor, its spec-driven development tool for the terminal, is becoming a plugin rather than a Gemini CLI extension, so that it can be driven conversationally and used from other agent tools such as Antigravity CLI."
  author: ["Mahima Shanware", "Sherzat Aitbayev", "Jay Kornder"]
  datePublished: "2026-07-16"
  publisher: "[[Organization/google]]"
---

This post announces the next stage of [[SoftwareApplication/conductor-gemini-cli-extension]], which Google introduced the previous year to bring [[DefinedTerm/spec-driven-development]] to the terminal by moving project awareness out of ephemeral chat logs and into persistent, version-controlled Markdown files. Conductor is changing from a Gemini CLI extension into the Conductor Plugin — a package that, as the post describes plugins, can include skills, rules, MCP servers and hooks together.

Two changes follow from that, according to the post. Conductor stops requiring strict command sequences and works conversationally, generating context, specs and plans as the developer discusses a feature; and it is no longer tied to Gemini CLI, so it can be used from [[SoftwareApplication/antigravity-cli]] and other tools. The post presents both as keeping the procedural rigor of spec-driven development while removing friction from it.

## Key Points

- The persistent Markdown artifacts stay: `spec.md` and `plan.md` are still produced, but creating and iterating on them is meant to feel like chatting with an assistant.
- Conductor is described as deciding for itself when to update the project's context or check off a completed task in the plan, managing project state in the background while the developer focuses on architecture.
- As a plugin, Conductor is presented as portable across tools: foundational documents on the project's architecture, guidelines and goals, together with shared configuration and ongoing development tracks, persist so that work started in one tool can be continued in another.
- Backwards compatibility is claimed with old Conductor commands and with existing plans and specs.
- The post names Antigravity CLI and Claude as tools the plugin can be used in.
- Google claims the Conductor Plugin achieved a higher success rate than a user not using spec-driven development on the most complex subset of [[Dataset/terminal-bench]] tasks. The post gives no figures, task counts or method for this comparison.
- Installation is from the plugin's GitHub repository, or into Antigravity CLI with `agy plugins install https://github.com/gemini-cli-extensions/conductor`; a hands-on Codelab is also offered.

## Context

The post is Google's announcement of a change to its own tool, and its performance claim is stated without supporting data. It restates Conductor's mission as helping make AI development "safe, predictable, and architecturally sound", and treats the repository as the single source of truth for a project, with the plugin changing how a developer interacts with that truth rather than where it lives.
