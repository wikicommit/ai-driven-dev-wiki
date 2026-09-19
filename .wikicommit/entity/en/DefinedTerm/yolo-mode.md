---
title: "YOLO Mode"
type: "schema:DefinedTerm"
lang: en
tags: [coding-agents, sandboxing, agent-safety]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Sep/30/designing-agentic-loops/'
    hash: sha256:616bc39546fd4aab969e3a8ec0a6fa01330405714c063a028ab4419f84132964
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A coding agent's setting in which every command it runs is approved by default rather than prompted for. Named this way by Simon Willison as a general label for the per-tool versions of the setting; described as simultaneously very dangerous and key to getting the most productive results."
---

YOLO mode is the mode of operation in which a coding agent's commands are all approved by default,
rather than the agent stopping to ask before each one. The name is the one Simon Willison says he
likes to use for the setting that each of these tools provides in its own version. Its significance
in the source is that it sits on both sides of a trade-off at once: it is described as *so dangerous*
and at the same time as key to getting the most productive results, because agents solve problems by
iterating and per-command approval is what stops them from iterating.

## Usage

The mode is discussed as the enabling condition for [[DefinedTerm/designing-agentic-loops]]. Agents
are characterised as inherently dangerous — able to make poor decisions or to fall victim to
[[DefinedTerm/prompt-injection]] — and since the most powerful tool a coding agent has is running a
command in the shell, an agent gone wrong can do anything its operator could do by running a command
themselves. Approval prompts are the default response to this, and the source's complaint about them
is not that they are tedious but that they blunt the brute-force iteration that makes agents useful.

Three risks are named for running unattended in this mode: shell commands that delete or mangle
things that matter; exfiltration attacks that steal files or data visible to the agent, with source
code and secrets in environment variables singled out as particularly exposed; and use of the machine
as a proxy to attack a third party, whether for denial of service or to disguise the origin of other
attacks.

Against those, three options are offered. The first is a secure sandbox restricting the files,
secrets and network the agent can reach (see [[DefinedTerm/sandboxing]]); the source judges Docker or
Apple's container tool a reasonable risk for most people, while noting that container escapes exist.
The second is using someone else's computer, so that a rogue agent has a bounded blast radius — the
author's own preference, with GitHub Codespaces given as his instance of it and the worst case
bounded as exfiltration of checked-out code or bad code pushed to the attached repository. The third
is simply taking the risk, which the source states is what most people choose.

## Related Terms

[[DefinedTerm/sandboxing]], [[DefinedTerm/designing-agentic-loops]], [[DefinedTerm/permission-modes]],
[[DefinedTerm/prompt-injection]], [[DefinedTerm/approval-fatigue]], [[DefinedTerm/human-in-the-loop]]
