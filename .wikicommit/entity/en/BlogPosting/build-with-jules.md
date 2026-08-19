---
title: "Build with Jules, your asynchronous coding agent"
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, ai-assisted-programming]
sources:
  - type: url
    url: 'https://blog.google/innovation-and-ai/models-and-research/google-labs/jules/'
    hash: sha256:600f7a1ec8134e15607bb66edb2851d78e361864e2e6017d9ccec7914744aafc
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Google Labs post of 20 May 2025 announcing that Jules, its asynchronous coding agent, was entering public beta with no waitlist, and setting out its cloud-VM architecture, GitHub integration and audio changelogs."
  author: ["Kathy Korevec"]
  datePublished: "2025-05-20"
  publisher: "Google"
---

"Build with Jules, your asynchronous coding agent" is a post of 20 May 2025 on Google's blog, in the Google Labs section, by Kathy Korevec, Director of Product Management at Google Labs. It announces that [[SoftwareApplication/jules]] is "entering public beta, available to *everyone*. No waitlist. Worldwide, everywhere where the Gemini model is available."

The post's argument for why the announcement matters is a claim about the field rather than about the product: "We're at a turning point: agentic development is shifting from prototype to product and quickly becoming central to how software gets built." Its description of Jules is framed as a rejection of the previous generation of tooling — "Not a co-pilot, not a code-completion sidekick, but an autonomous agent that reads your code, understands your intent, and gets to work" — and it notes Jules had been introduced in Google Labs the previous December as "an early glimpse of what a true coding agent could become".

## Key Points

- Jules is described as an asynchronous, agentic coding assistant that integrates directly with existing repositories, clones the codebase into a secure Google Cloud virtual machine, understands the full context of the project, and performs tasks including writing tests, building new features, providing audio changelogs, fixing bugs and bumping dependency versions.
- It operates asynchronously so the developer can work on something else, and on completion presents its plan, its reasoning and a diff of the changes made.
- Privacy is stated as a default: Jules does not train on private code and data stays isolated within the execution environment.
- It runs on Gemini 2.5 Pro, which the post says gives it access to some of the most advanced coding reasoning available, and which paired with the cloud VM system lets it handle complex multi-file changes and concurrent tasks.
- The six capabilities the post lists are: working on real codebases without needing a sandbox; parallel execution of concurrent tasks inside the cloud VM; a visible workflow showing the plan and reasoning before changes; GitHub integration with no context-switching or extra setup; user steerability, with the plan modifiable before, during and after execution; and audio summaries turning recent commits into a listenable changelog.
- Access during the public beta is free of charge with usage limits applying, and Google says it expects to introduce pricing after the beta as the platform matures.

## Context

Every capability claim here is Google's own, published in its product announcement; the post contains no independent evaluation, no benchmark figures and no comparison against other agents. The page also carries a machine-generated summary that Google labels as produced by Google AI and marks as experimental — a detail worth noting on a post announcing an autonomous coding agent, since it is the vendor applying the same class of automation to its own communications.

The post positions itself as the second stage of an announcement it says began the previous December, when Jules was introduced in Google Labs as "an early glimpse of what a true coding agent could become" — a characterisation this post gives without further detail. What changed between the two stages is recorded on [[SoftwareApplication/jules]], which also cites the earlier announcement.
