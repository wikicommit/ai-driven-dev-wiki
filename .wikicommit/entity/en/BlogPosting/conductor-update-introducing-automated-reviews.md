---
title: "Conductor Update: Introducing Automated Reviews"
type: "schema:BlogPosting"
lang: en
tags: [agents, code-review, coding-tools]
sources:
  - type: url
    url: 'https://developers.googleblog.com/conductor-update-introducing-automated-reviews/'
    hash: sha256:3cd3c8c42c60d393ffc49d407101f5f4b337eb9aea4a3b31a8b17e4304bac338
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Google's announcement of an Automated Review feature for Conductor, extending the Gemini CLI extension from planning and execution into a post-implementation validation step that reports on code quality and compliance with the project's own plan, spec and guideline files."
  author: ["Sherzat Aitbayev", "Mahima Shanware", "Jay Kornder"]
  datePublished: "2026-02-13"
  publisher: "[[Organization/google]]"
---

This post announces an Automated Review feature for [[SoftwareApplication/conductor-gemini-cli-extension]], the Gemini CLI extension Google introduced in December to bring context-driven development to the terminal. The post's stated framing for the original extension is that it shifts project awareness out of ephemeral chat logs and into persistent, version-controlled markdown files, which it credits with helping developers plan before they build.

The new feature's purpose is given as making AI-assisted engineering safer and more predictable by taking Conductor beyond planning and execution into validation. Once a coding agent completes its tasks, Conductor can generate a post-implementation report on code quality and on compliance with guidelines the developer has defined.

The post's closing argument is about the division of labour the feature is meant to enforce: that this level of detail "ensures that 'agentic' development doesn't mean 'unsupervised' development", producing a workflow in which the AI provides the labour and the developer provides high-level architectural oversight backed by automated verification.

## Key Points

- Automated Review is presented as adding a "verify" step to the development lifecycle, run after the coding agent finishes rather than during implementation.
- Five capabilities are listed for the report: code review, plan compliance, guideline enforcement, test-suite validation, and a basic security review.
- The code-review capability is described as deep static and logic analysis of newly generated files, going beyond syntax to proactively flag complex issues such as race conditions in asynchronous blocks, potential null pointer risks, and logic errors that could lead to runtime exceptions — the post gives these as examples rather than as the full set.
- Plan compliance is described as checking new code against the project's `plan.md` and `spec.md` to confirm every phase of the roadmap was addressed and no core requirements were omitted.
- Test-suite validation is described as running the relevant unit and integration tests within the review workflow and folding the results and coverage data into the final report, rather than relying on manual execution.
- The security review is described as scanning for critical vulnerabilities before code is merged, automatically flagging high-risk issues such as hardcoded API keys, potential personally identifiable information leaks, or unsafe input handling that could expose the application to injection attacks — again given as examples. The post calls this a "basic" security review rather than a comprehensive one.
- Findings are categorized by severity as High, Medium or Low, and come with the exact file path; a track can be started within Conductor to fix them.
- These are Google's own claims about its own extension, stated as capabilities rather than as measured results — the post reports no evaluation, benchmark or error rate for any of the five checks.

## Context

The post positions the feature as a follow-up to Conductor's December introduction rather than as a new product, and describes the extension as "evolving rapidly". It states no version number for the release and gives no date for the Automated Review feature's availability beyond the post's own publication.

Its stated commitment is to making AI development "safe, predictable, and architecturally sound", and it closes with installation instructions: the extension's repository at <https://github.com/gemini-cli-extensions/conductor>, or the command `gemini extensions install https://github.com/gemini-cli-extensions/conductor`.
