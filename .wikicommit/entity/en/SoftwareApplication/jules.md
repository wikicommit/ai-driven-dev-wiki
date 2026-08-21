---
title: "Jules"
type: "schema:SoftwareApplication"
lang: en
tags: [agentic-coding, ai-assisted-programming]
sources:
  - type: url
    url: 'https://developers.googleblog.com/en/the-next-chapter-of-the-gemini-era-for-developers/'
    hash: sha256:14b103534d56b72c11ed40d81d382de5a7a3e724fdc4de1f2a18de4524165941
  - type: url
    url: 'https://blog.google/innovation-and-ai/models-and-research/google-labs/jules/'
    hash: sha256:600f7a1ec8134e15607bb66edb2851d78e361864e2e6017d9ccec7914744aafc
  - type: url
    url: 'https://addyosmani.com/blog/code-agent-orchestra/'
    hash: sha256:399fcd256a0dea0d4dc0841558f7f17cf41a9b447bc6bbc5adfbaf8728e9c557
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An asynchronous coding agent from Google Labs, introduced in December 2024 and entering public beta on 20 May 2025. It clones a repository into a Google Cloud VM, works in the background, and returns a plan, its reasoning and a diff; it integrates with GitHub and runs on Gemini 2.5 Pro."
  applicationCategory: "Asynchronous coding agent"
  author: "Google Labs"
  operatingSystem: "Cloud (Google Cloud VM)"
---

Jules is an asynchronous coding agent from Google Labs. Its own framing is set against code completion rather than alongside it: Google describes it as "Not a co-pilot, not a code-completion sidekick, but an autonomous agent that reads your code, understands your intent, and gets to work." It integrates directly with existing repositories, clones the codebase into a secure Google Cloud virtual machine, works in the background while the developer does something else, and on completion presents its plan, its reasoning and a diff of the changes made.

The tasks Google lists for it are writing tests, building new features, providing audio changelogs, fixing bugs and bumping dependency versions. At public beta it ran on Gemini 2.5 Pro, which Google says gives it access to some of the most advanced coding reasoning available; at introduction it was described as an experimental agent that "will use Gemini 2.0", limited to Python and JavaScript coding tasks.

## Overview

The design choices Google emphasises are about where the work happens and how much of it the developer sees. Jules is stated to be private by default — it does not train on private code, and data stays isolated within the execution environment. Google claims it "doesn't need a sandbox", taking the full context of an existing project to reason about changes, and that running tasks inside a cloud VM enables concurrent execution of multiple requests. On control, it shows its plan and reasoning before making changes and lets the developer modify that plan before, during and after execution; the introduction post described it as creating comprehensive multi-step plans, modifying multiple files, and preparing pull requests to land fixes back into GitHub.

GitHub integration is presented as the point of contact: Jules "works where you already do, directly inside your GitHub workflow", with what Google describes as no context-switching and no extra setup. The audio changelog is the more unusual feature — an audio summary of recent commits, turning project history into something the developer can listen to.

These are Google's own claims for its own product, made in launch and beta announcements; the sources here contain no independent evaluation of them, and the introduction post itself carried the caveat that "Jules may make mistakes."

## Features

- Repository integration with cloning into a secure Google Cloud VM.
- Asynchronous background execution, with parallel execution of concurrent tasks inside the VM.
- A visible plan and reasoning presented before changes, and a diff on completion.
- User steerability: the plan can be modified before, during and after execution.
- GitHub workflow integration, including preparing pull requests.
- Audio changelogs of recent commits.
- Private by default, with no training on private code and data isolated to the execution environment.

### As a Tier 3 cloud agent

[[BlogPosting/the-code-agent-orchestra]] places Jules among the cloud async agents — tools where a task is assigned and the developer returns to a pull request, with no terminal or local setup. Its description of the workflow matches the plan-first shape above: connect a GitHub repository, describe a task, approve the plan Jules generates before any code is written, then let it run in a cloud VM and return a pull request with full reasoning and terminal logs. The distinctive features it names are audio changelogs, mid-task interruption, and the Jules Tools CLI for piping GitHub issues directly, and it records that Jules reads a repository's [[DefinedTerm/agents-md]] file automatically with no extra configuration.

## History

Jules was introduced in Google Labs in December 2024, in [[Organization/google]]'s "The next chapter of the Gemini era for developers" post, as an experimental AI-powered code agent available to a select group of trusted testers, with wider availability promised for other interested developers in early 2025. That post situated it inside a broader claim about the field — "As AI code assistance rapidly evolves from simple code searches to AI-powered assistants embedded in developer workflows, we want to share the latest advancement that will use Gemini 2.0" — and reported alongside it a research result of 51.8% on [[Dataset/swe-bench]] Verified using Gemini 2.0 Flash equipped with code execution tools.

That introduction also stated three benefits Google reported from its own internal use, which are worth recording as the vendor's original claims for the product rather than as observed outcomes: **more productivity**, from assigning issues and coding tasks for asynchronous execution; **progress tracking**, through real-time updates that let a developer prioritise what needs attention; and **full developer control**, meaning reviewing the plans Jules creates along the way, giving feedback or requesting adjustments, and reviewing before merging. The last of these — review of the plan, not only of the diff — is the earliest statement of the human-checkpoint shape the tool has kept.

On 20 May 2025 Jules entered public beta in [[BlogPosting/build-with-jules]], available to everyone with no waitlist, worldwide wherever the Gemini model is available. Google's framing there was that "agentic development is shifting from prototype to product and quickly becoming central to how software gets built." Access during the beta was free of charge with usage limits applying, and Google said it expected to introduce pricing after the beta as the platform matured.
