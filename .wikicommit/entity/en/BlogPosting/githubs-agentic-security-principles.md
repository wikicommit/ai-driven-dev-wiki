---
title: "How GitHub's agentic security principles make our AI agents as secure as possible"
type: "schema:BlogPosting"
lang: en
sources:
  - type: url
    url: 'https://github.blog/ai-and-ml/github-copilot/how-githubs-agentic-security-principles-make-our-ai-agents-as-secure-as-possible/'
    hash: sha256:4d060e60394d3bb5b60078b4750eb96bd19bc3ec2961726e242bb6398e575bee
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"
tags: [agent-safety, security, prompt-injection, guardrails, human-oversight]

properties:
  description: "GitHub's account of the threat model and six design rules behind its hosted agentic products: maximize interpretability, minimize autonomy, and keep a human in the loop for anything irreversible."
  author: ["Rahul Zhade"]
  datePublished: "2025-11-25"
  publisher: "[[Organization/github]]"
---

GitHub's account of the security guidelines behind its hosted AI agents, written from the
premise that usability and security are in tension: the more agentic a product is, the more
it can do and the richer the workflows it enables, but the greater the chance and impact of
the AI going off its guardrails, losing alignment, or being manipulated by a bad actor. The
author states the guidelines exist to ensure there is always a
[[DefinedTerm/human-in-the-loop]] element in everything GitHub designs.

The post states three design goals for GitHub's hosted agents — maximize interpretability,
minimize autonomy, and reduce anomalous behaviour — then sets out a threat model in three
risk classes and six rules applied across GitHub's hosted agentic products, with
[[SoftwareApplication/github-copilot-coding-agent]] as the worked example. The post offers
the principles from the outset as something readers might apply to their own agents, and
says at the end that they were built to be applicable to any new AI product.

## Key Points

- **Risk 1, data exfiltration**: an agent with internet access could leak context to
  unintended destinations, inadvertently or maliciously. The post's severe example is an
  agent leaking a write-access GitHub token to a malicious endpoint.
- **Risk 2, impersonation and action attribution**: when an agent acts, it may not be clear
  what permissions it should have or under whose direction it operates. The post's example
  asks who issued the directive when Copilot is assigned to an issue — the person who filed
  it or the person who assigned it — and how accountability and traceability are preserved
  if an incident results.
- **Risk 3, [[DefinedTerm/prompt-injection]]**: because agents are prompted from issues,
  files in a repository and many other places, the post argues the initiating user needs a
  clear picture of *all* the information guiding the agent, or malicious users could hide
  directives and trick maintainers into running agents with bad ones.
- **Rule 1, ensure all context is visible**: GitHub displays the files context is generated
  from, and attempts to strip invisible or masked information carried via Unicode or HTML
  tags before it reaches the agent. Its stated example of the attack is a GitHub issue
  containing invisible Unicode with injected instructions, which a maintainer would assign
  to Copilot without seeing them.
- **Rule 2, firewall the agent**: a firewall limits the coding agent's access to potentially
  harmful external resources and lets users configure network access and block unwanted
  connections; the post states that MCP interactions are automatically allowed to bypass the
  firewall, as a balance between security and usability. Under the same rule the post gives a
  separate control in a different product: in Copilot Chat code is not executed automatically
  — generated HTML is presented as code for preview, and a user must manually enable the rich
  previewing interface that executes it.
- **Rule 3, limit access to sensitive information**: the post's formulation is that the
  easiest way to stop exfiltration is not to grant the access in the first place. CI secrets
  and files outside the current repository are not automatically passed to agents, and the
  coding agent's GitHub token is revoked once its session completes.
- **Rule 4, prevent irreversible state changes**: on the stated premise that AI can and will
  make mistakes, agents cannot initiate irreversible state changes without a human in the
  loop. The coding agent can only create pull requests and cannot commit directly to a
  default branch; its pull requests do not run CI automatically, requiring a human to
  validate the code and manually run GitHub Actions; and in Copilot Chat, MCP interactions
  ask for approval before any tool call.
- **Rule 5, attribute actions to both initiator and agent**: interactions are attributed to
  the initiating user and actions to the agent, which the post frames as a clear chain of
  responsibility. Pull requests from the coding agent are co-committed by the initiating
  user and generated using the Copilot identity to make clear they were AI-generated.
- **Rule 6, gather context only from authorized users**: agents operate under the permissions
  and context of the user who initiated the interaction. The coding agent can only be
  assigned to issues by users with write access to the repository, and — the post notes this
  matters especially for public repositories — reads issue comments only from users with
  write access.

## Context

This is a first-party account of GitHub's own security design on GitHub's own blog, and it
describes controls the vendor says it has implemented rather than reporting any external
audit, penetration test or measurement of their effectiveness. The post itself frames the
principles as design decisions intended to be invisible to end users, offered for
transparency.

Related terms in this wiki: [[DefinedTerm/indirect-prompt-injection]],
[[DefinedTerm/guardrails]], [[DefinedTerm/safe-outputs]],
[[DefinedTerm/deny-first-permission-evaluation]] and [[DefinedTerm/sandboxing]].
