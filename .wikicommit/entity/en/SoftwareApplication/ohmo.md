---
title: "ohmo"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-tooling]
sources:
  - type: url
    url: 'https://github.com/HKUDS/OpenHarness'
    hash: sha256:9bbda0914ba868f48d4405712010871672d985e50cc184e63fbbbd2d0a88071e
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A personal AI agent from HKUDS, built on OpenHarness and packaged alongside it, that users talk to through chat apps such as Feishu, Slack, Telegram and Discord, and that runs on an existing Claude Code or Codex subscription."
  applicationCategory: "Personal AI agent"
  author: "HKUDS"
---

ohmo is a personal AI agent built on [[SoftwareApplication/openharness]] and packaged in the same repository. Its README describes it as "not another chatbot, but an assistant that actually works for you over long sessions": users chat with it in Feishu, Slack, Telegram or Discord, and it forks branches, writes code, runs tests and opens pull requests on its own. It runs on an existing [[SoftwareApplication/claude-code]] subscription or Codex subscription, so no extra API key is needed.

## Capabilities

ohmo keeps a personal workspace under `~/.ohmo`, created once with `ohmo init`. Files there hold the agent's long-term personality and behaviour (`soul.md`), who ohmo is (`identity.md`), the user's profile and preferences (`user.md`), a first-run bootstrap ritual (`BOOTSTRAP.md`), a personal memory directory, and a gateway configuration recording the selected provider profile and channels. `ohmo config` sets up channels and the model provider using the same workflow choices as OpenHarness's own setup, and can restart a running gateway after a change; the gateway is what connects the agent to the chat apps, and it can be started, run in the foreground, checked and restarted from the command line. OpenHarness releases in April 2026 added channel slash commands, file attachments and multimodal messages to ohmo's channels.
