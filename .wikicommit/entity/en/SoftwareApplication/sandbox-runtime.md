---
title: "Sandbox Runtime"
type: "schema:SoftwareApplication"
lang: en
tags: [sandboxing, security]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/claude-code-sandboxing'
    hash: sha256:fb32cb34826801c245ce18f24b54cbb117f8099475c3cf01237f9d74484d7abb
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Anthropic's open-source sandbox runtime, released as a research preview, that restricts which directories and network hosts a process can access using OS-level primitives; Claude Code uses it to sandbox its bash tool."
  applicationCategory: "Sandbox runtime"
  operatingSystem: "Linux, macOS"
  author: "[[Organization/anthropic]]"
---

Sandbox Runtime is a sandbox for agents and other processes introduced by [[Organization/anthropic]] in [[BlogPosting/beyond-permission-prompts]]. It lets a user define exactly which directories and network hosts an agent can access, without the overhead of spinning up and managing a container. It was released in beta as a research preview and is also available as an open-source research preview.

[[SoftwareApplication/claude-code]] uses it to sandbox its bash tool, so that Claude can execute commands inside the limits the user has set without permission prompts; the runtime can also be used to sandbox arbitrary processes, agents and MCP servers.

## Capabilities

The runtime enforces its restrictions at the operating-system level, built on Linux bubblewrap and macOS seatbelt, and the restrictions apply not only to the process it launches but to any scripts, programs or subprocesses that process spawns. As configured for Claude Code's bash tool it enforces two boundaries:

- **Filesystem isolation** — read and write access to the current working directory, with modification of any files outside it blocked.
- **Network isolation** — internet access only through a unix domain socket connected to a proxy server running outside the sandbox. The proxy restricts which domains a process can connect to and handles user confirmation for newly requested domains, and it can be customized to enforce arbitrary rules on outgoing traffic.

Both boundaries are configurable, allowing or disallowing specific file paths or domains. When a sandboxed command tries to access something outside the sandbox, the user is notified immediately and can choose whether to allow it. In Claude Code it is started with the `/sandbox` command.

## Adoption & Ecosystem

Anthropic reports that in its internal usage, sandboxing Claude Code this way reduced permission prompts by 84%. It open-sourced the runtime so that other teams can build safer agents, and recommends that others consider adopting it for their own agents. The runtime is the concrete implementation behind the OS-level form of [[DefinedTerm/sandboxing]] discussed elsewhere in this wiki.
