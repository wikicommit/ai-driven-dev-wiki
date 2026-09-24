---
title: "Gemini CLI"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, cli]
sources:
  - type: url
    url: 'https://addyosmani.com/blog/future-agentic-coding/'
    hash: sha256:b6fa751c05fa1595dabeb21c14458cf4c51a1dd2997ce1edb3920fd3cebddf4a
  - type: url
    url: 'https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/'
    hash: sha256:74ccc5f44492281655fe5a0f8252a401ded3c57354ca7f1efbbcc7b28d3120f6
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Google's terminal-based AI coding assistant powered by Gemini models, used for planning and coding against a codebase from an interactive shell session. Google announced that from June 18, 2026 it would no longer serve consumer users, who are moved to Antigravity CLI, while enterprise and paid-API use continues."
  applicationCategory: "Command-line coding assistant"
  author: "[[Organization/google]]"
---

Gemini CLI is a command-line assistant from [[Organization/google]], powered by its Gemini models, that brings an AI agent into the developer's terminal. A developer prompts it from a shell session — to analyze a codebase, or to draft a solution plan — and then iterates on the results interactively, directing each step. Google released it in 2025, and in May 2026 announced that it was consolidating its terminal agent work into [[SoftwareApplication/antigravity-cli]], moving consumer users of Gemini CLI there while keeping Gemini CLI available to enterprise customers ([[BlogPosting/transitioning-gemini-cli-to-antigravity-cli]]).

## Capabilities

It is invoked from the command line and works against an existing codebase; analyzing a codebase and drafting a solution plan are the two uses one account names, with its large context window singled out as the characteristic feature and the developer refining the output across successive turns of the same session. Google's own account names Agent Skills, hooks, subagents and extensions among its features, and credits its terminal UI and weekly release cadence with being what users liked about it.

## Adoption & Ecosystem

[[BlogPosting/future-of-agentic-coding-conductors-to-orchestrators]] groups Gemini CLI with the conductor-style tools — alongside [[SoftwareApplication/claude-code]], [[SoftwareApplication/cursor]] and in-IDE chat assistants — on the grounds that the human directs each step and the tool responds within the session. That post describes it as a one-at-a-time collaborator that does not go off and make code changes on its own, while explicitly hedging that this holds for the conductor mode it is discussing rather than for the tool in general.

Google's own explanation for the transition is that users' workflows outgrew it: they now want several agents communicating with each other to split up work, which needs terminal tools that share a backend with the rest of the workflow. Google announced that on June 18, 2026, Gemini CLI and the Gemini Code Assist IDE extensions would stop serving requests for Google AI Pro and Ultra subscribers and for free users of Gemini Code Assist for individuals. Organizations using Gemini CLI under a Gemini Code Assist Standard or Enterprise license keep their access, with Google stating it will continue to support it with the latest Gemini models, and it remains usable through paid Gemini and Gemini Enterprise Agent Platform API keys. Antigravity CLI carries over Gemini CLI's Agent Skills, hooks and subagents, with its extensions becoming Antigravity plugins, though Google said feature parity would not be one-to-one at first.
