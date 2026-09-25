---
title: "Beyond permission prompts: making Claude Code more secure and autonomous"
type: "schema:BlogPosting"
lang: en
tags: [security, sandboxing, agent-permissions]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/claude-code-sandboxing'
    hash: sha256:fb32cb34826801c245ce18f24b54cbb117f8099475c3cf01237f9d74484d7abb
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An Anthropic engineering post introducing two sandboxing features for Claude Code — a sandboxed bash tool and Claude Code on the web — which enforce filesystem and network isolation so the agent can run with fewer permission prompts."
  author: ["David Dworken", "Oliver Weller-Davies"]
  datePublished: "2025-10-20"
  publisher: "[[Organization/anthropic]]"
---

The post starts from [[SoftwareApplication/claude-code]]'s permission-based model: by default the agent is read-only and asks before modifying anything or running most commands, with a few safe commands such as `echo` or `cat` auto-allowed. It argues that constantly clicking "approve" both slows development and can lead to [[DefinedTerm/approval-fatigue]], where users stop paying close attention to what they approve — making development less safe rather than more.

Its answer is [[DefinedTerm/sandboxing]]: pre-defined boundaries inside which Claude can work freely instead of asking permission for each action. The post introduces two features built on this idea. The first is a sandboxed bash tool, running on a new sandbox runtime ([[SoftwareApplication/sandbox-runtime]]) released as a beta research preview and as open source. The second is [[SoftwareApplication/claude-code-for-web]], which runs each Claude Code session in an isolated sandbox in the cloud. Anthropic reports that in its internal usage sandboxing safely reduced permission prompts by 84%.

## Key Points

- The sandboxing approach enforces two boundaries built on operating-system-level features: filesystem isolation, so Claude can only access or modify specific directories, and network isolation, so it can only connect to approved servers.
- Effective sandboxing is said to require both: without network isolation a compromised agent could exfiltrate files such as SSH keys, and without filesystem isolation it could escape the sandbox and gain network access.
- The motivating threat is [[DefinedTerm/prompt-injection]]: filesystem isolation stops a prompt-injected Claude from modifying sensitive system files, and network isolation stops it from leaking information or downloading malware.
- The sandbox runtime lets users define which directories and network hosts an agent can access without spinning up and managing a container, and can sandbox arbitrary processes, agents and MCP servers.
- In Claude Code it sandboxes the bash tool: inside the sandbox commands run without permission prompts, and an attempt to reach something outside it notifies the user, who can choose whether to allow it.
- Enforcement uses OS primitives — Linux bubblewrap and macOS seatbelt — and covers not only Claude Code's direct actions but any scripts, programs or subprocesses a command spawns.
- By default the bash sandbox allows reads and writes in the current working directory and blocks modification of files outside it; network access goes only through a unix domain socket connected to a proxy outside the sandbox, which restricts reachable domains and asks the user about newly requested ones. Both sides are configurable.
- The post claims that sandboxing ensures even a successful prompt injection is fully isolated, so a compromised Claude Code cannot steal SSH keys or phone home to an attacker's server.
- Claude Code on the web is designed so that sensitive credentials such as git credentials or signing keys are never inside the sandbox with Claude; a custom proxy handles git interactions, verifies a scoped credential and the content of each interaction (for example, pushing only to the configured branch), then attaches the real token before forwarding to GitHub.
- Anthropic open-sourced the sandbox feature and recommends that others building agents consider adopting it.

## Context

This is a vendor's own launch write-up for its own features: the 84% figure is from Anthropic's internal usage, and the security claims describe the design as its builders intend it. The argument it makes — that fewer prompts inside a hard boundary is safer than many prompts without one — reappears in this wiki's account of [[DefinedTerm/approval-fatigue]] and in other writing on [[DefinedTerm/sandboxing]], where the same design is discussed by third parties.
