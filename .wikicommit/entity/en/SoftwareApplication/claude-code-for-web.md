---
title: "Claude Code for web"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, anthropic, coding-tools, sandboxing]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Oct/20/claude-code-for-web/'
    hash: sha256:45fb7060c3561e36111229e2a76520baefc9e1538596494a73f3ba55f27fb826
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Anthropic's hosted, asynchronous form of Claude Code, run in a container managed by Anthropic against a GitHub repository and driven from a web and mobile interface, which opens a branch and optionally a pull request when it finishes."
  applicationCategory: "Asynchronous coding agent"
  featureList: "Runs against a GitHub repository in a hosted container; selectable network environments from no access to a custom domain allow-list; prompts queued while a run is in progress; opens a branch and optionally a pull request; teleport of transcript and edited files to the local CLI"
  author: "[[Organization/anthropic]]"
---

Claude Code for web is the hosted, asynchronous form of [[SoftwareApplication/claude-code]],
launched by Anthropic in October 2025 and available through the Claude web interface and as a tab in
the Claude iPhone app. What the source establishes outright is that it runs in a container managed by
Anthropic; its identification of what runs inside that container is offered as the author's own
inference from the outside — as far as he can tell, the Claude Code CLI wrapped in a container and
configured to skip permission prompts, which he reports appears to behave exactly like the local tool.

It belongs to the category of asynchronous coding agents, and the source positions it as Anthropic's
counterpart to OpenAI's Codex Cloud and [[SoftwareApplication/google-jules]], with a very similar
shape: point it at a repository, give it a prompt, and collect the result as a branch rather than
watching it work.

## Capabilities

A run is set up by pointing the agent at a GitHub repository, choosing an environment, and supplying
a prompt. While a run is in progress, further prompts can be sent and are queued for execution after
the current step completes. When the run finishes, the agent opens a branch on the repository
carrying its work and can optionally open a pull request. A "teleport" feature copies both the chat
transcript and the edited files down to the local Claude Code CLI, so a session started in the hosted
environment can be taken over locally.

The environment choice is the security-relevant control, and the source describes a range from fully
locked down, through a restricted allow-list of domains, to a configuration allowing domains of the
user's choosing including `*` for everything. The only run whose environment the source specifies is
at the open end of that range — a benchmark against a private repository under a custom `*`
allow-list, chosen because that project involved no secrets or source code needing protection. Separately it states that running
with no network access leaves nothing to worry about, and records unease about the default
allow-list of the middle setting.

## Notes

The source's assessment is that the pull requests it produces are indistinguishable from the local
CLI's — it reports that the same prompt would likely have given the same result on a laptop — and locates the
product's value entirely in convenience: a hosted container managed by Anthropic with a web and
mobile interface over it. The examples it gives are a small single-file tool, a README correction,
and a multi-scenario Python templating benchmark complete with charts, the last of these entered on a
phone keyboard.

On cost, the source declines to generalise, noting it was using a plan provided by Anthropic for
testing and estimating only its own daily CLI spend via an unofficial tool.

## Related

[[SoftwareApplication/claude-code]], [[DefinedTerm/sandboxing]], [[DefinedTerm/lethal-trifecta]], [[SoftwareApplication/google-jules]], [[SoftwareApplication/openai-codex]], [[BlogPosting/claude-code-for-web-async-coding-agent]]
