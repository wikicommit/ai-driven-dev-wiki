---
title: "Claude Cowork"
type: "schema:SoftwareApplication"
lang: en
tags: [sandboxing, security]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/how-we-contain-claude'
    hash: sha256:2f700ae2ec223a60449a0e82f0575d72c600c7a2d945aa408b3384763f2d15c1
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Anthropic's desktop agent for general knowledge work, which runs with access to a user-selected workspace folder and executes the agent's code inside a local virtual machine."
  applicationCategory: "AI agent"
  operatingSystem: "macOS, Windows"
  author: "[[Organization/anthropic]]"
---

Claude Cowork is one of [[Organization/anthropic]]'s three primary agentic products, alongside claude.ai and [[SoftwareApplication/claude-code]]. It runs on a user's desktop with access to a workspace folder the user selects, and is built for general knowledge work rather than software engineering. Its containment design is described in [[BlogPosting/how-we-contain-claude-across-products]].

Because its typical user is much less likely to be fluent in bash than a Claude Code user, the post argues that per-action human approval does not transfer: a non-technical knowledge worker should not be expected to judge shell commands. Cowork instead relies on a boundary that is absolute and always on — a local virtual machine.

## Capabilities

The first version of Cowork ran inside a full virtual machine using the platform's vendor hypervisor — Apple's Virtualization framework on macOS and HCS on Windows. The VM has its own Linux kernel, filesystem and process table; only the user's selected workspace and `.claude` folder are mounted, and nothing else on the host is visible. Credentials stay in the host's keychain and never enter the guest; the VM gets a per-session, scoped-down token that can be revoked independently of the user's.

In that original "full-VM mode" the agent loop itself ran inside the guest, so there was no outer process with the authority to grant an exception to the sandbox. Because any failure during VM startup made Cowork unusable, the agent loop was later moved outside the VM while code execution stayed inside it, so the VM still enforces filesystem and network controls over code the agent runs. Local MCP servers were also moved outside the VM, treated like any software a user might install, with admins deciding which to enable.

Workspace folders can be mounted read-only, read-write, or read-write-no-delete, and enterprise admins can restrict mount paths through allowlists in MDM settings. Traffic to Anthropic's API passes through a defensive man-in-the-middle proxy inside the VM that accepts only the VM's own session token and blocks headers that would enable server-side fetch.

## Adoption & Ecosystem

The post records two lessons from operating Cowork. A third-party disclosure showed that allowing `api.anthropic.com` through the egress allowlist let a malicious file in the workspace direct Claude to upload files to an attacker's account using the attacker's API key; the in-VM proxy was the fix. And enterprise security teams found that the VM's isolation also kept host-based endpoint detection and response tools from seeing inside it; the current mitigation is pull-based OTLP exports that let administrators retrieve event logs after the fact, which the post notes is not the same as live monitoring.
