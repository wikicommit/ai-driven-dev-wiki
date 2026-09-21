---
title: "Conductor (Gemini CLI extension)"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, code-review, coding-tools, spec-driven-development]
sources:
  - type: url
    url: 'https://developers.googleblog.com/conductor-update-introducing-automated-reviews/'
    hash: sha256:3cd3c8c42c60d393ffc49d407101f5f4b337eb9aea4a3b31a8b17e4304bac338
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An extension for the Gemini CLI that keeps project context in persistent, version-controlled markdown files rather than in ephemeral chat logs, and — since its Automated Review feature — also generates a post-implementation report checking the resulting code against the project's plan and spec files."
  applicationCategory: "Coding-agent extension"
  featureList: "Context-driven planning; automated post-implementation review covering code quality, plan compliance, guideline enforcement, test-suite validation and a basic security scan"
  author: "[[Organization/google]]"
---

Conductor is an extension for the Gemini CLI, introduced by Google in the December preceding its February 2026 update, whose stated aim is to bring context-driven development to the terminal. Its central design choice is where project awareness lives: rather than accumulating in ephemeral chat logs, it is shifted into persistent, version-controlled markdown files — `plan.md` and `spec.md` are the two the source names. Google credits this with helping developers plan before they build.

With the Automated Review feature announced in February 2026, the extension covers validation as well as planning and execution. Once a coding agent completes its tasks, Conductor can generate a post-implementation report on code quality and on compliance with the guidelines the developer has defined.

The extension is installed from its GitHub repository, either directly or with `gemini extensions install https://github.com/gemini-cli-extensions/conductor`.

## Capabilities

The planning side is described only in outline in the source used here: project context is kept in version-controlled markdown files that the workflow then works from.

The Automated Review side is described in more detail, as five checks that make up a single post-implementation report:

- **Code review** — deep static and logic analysis of newly generated files, going beyond syntax to flag complex issues such as race conditions in asynchronous blocks, potential null pointer risks, and logic errors that could lead to runtime exceptions.
- **Plan compliance** — checking the new code against `plan.md` and `spec.md` to confirm every phase of the roadmap was addressed and that no core requirements were omitted during coding.
- **Guideline enforcement** — verifying that new contributions adhere to the project's style guides and to any custom guideline files generated during the planning phase.
- **Test-suite validation** — running the relevant unit and integration tests as part of the review workflow and incorporating the results and coverage data into the report, instead of relying on manual execution.
- **Basic security review** — scanning for critical vulnerabilities before code is merged, flagging high-risk issues such as hardcoded API keys, potential personally identifiable information leaks, or unsafe input handling that could expose the application to injection attacks.

Findings are graded High, Medium or Low and carry the exact file path, and a track can be started within Conductor to work through them. No version number is stated for any of this behaviour, and the capabilities are Google's own description rather than measured results.

## Adoption & Ecosystem

Conductor runs as an extension of the Gemini CLI rather than as a standalone tool, so it inherits that assistant's terminal-based way of working. Its `plan.md` / `spec.md` convention places it alongside the broader practice of [[DefinedTerm/spec-driven-development]], and the review step it adds is an instance of [[DefinedTerm/agentic-code-review]] run against those same specification files rather than against a reviewer's own judgment alone.

Google frames the arrangement as keeping agentic development supervised: the AI supplies the labour while the developer supplies high-level architectural oversight, backed by automated verification. The announcement is reported in [[BlogPosting/conductor-update-introducing-automated-reviews]].
