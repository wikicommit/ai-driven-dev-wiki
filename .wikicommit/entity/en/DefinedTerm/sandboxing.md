---
title: "Sandboxing"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/agentic-engineering/sandboxing/'
    hash: sha256:fa1d62f87add57f7ca59294cf760dfbbfcf9a829c2af19ebb1535d78ede47485
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "The practice of running an AI coding agent in an isolated environment — a container, VM, separate branch, or disposable workspace — so its actions can't affect production systems or the real codebase."
---

Sandboxing is the practice of running an AI coding agent in an isolated environment — a container, a virtual machine, a separate branch, or a disposable workspace — where it can read files, write code, and run commands without affecting real production systems. If the agent makes a mistake, such as deleting a directory, corrupting a config file, or installing a bad dependency, the damage is contained to the sandbox and the real codebase stays untouched.

## Usage

Concrete forms of sandboxing include: git worktrees (an isolated copy of the repository for the agent to work in, merged if the result is good and deleted otherwise), containers (running the agent inside Docker with limited network access and filesystem isolation), cloud sandbox services such as GitHub Codespaces or Gitpod providing ephemeral dev environments, branch-based isolation where the agent works on a separate branch and CI verifies the changes before human review, network restrictions preventing the agent from making external API calls or accessing production services, and permission scoping (read-only access for most directories, write access only to specific paths) as a lighter-weight form of isolation even without full sandboxing.

## When It Applies

Sandboxing matters more as an agent is given more autonomy: agents can misinterpret instructions, hallucinate solutions, or execute commands with unintended side effects, and without isolation every action carries real risk, so each command needs review and approval before it runs. With sandboxing in place, an agent can experiment freely and only the final result needs review, which is described as dramatically speeding up workflows. It is presented as a general best practice for autonomous agents rather than one party's specific proposal, summarized as treating agent output like an untrusted pull request: let it work in isolation, review the result, and merge only after verification.

## Related Terms

[[DefinedTerm/guardrails]], [[DefinedTerm/human-in-the-loop]], [[DefinedTerm/tool-use]], [[DefinedTerm/agentic-engineering]]
