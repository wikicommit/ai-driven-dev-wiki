---
title: "Skill Issue: Harness Engineering for Coding Agents"
type: "schema:BlogPosting"
lang: en
tags: [harness-engineering, context-engineering, coding-agents]
sources:
  - type: url
    url: 'https://www.humanlayer.dev/blog/skill-issue-harness-engineering-for-coding-agents'
    hash: sha256:210c3b64f14464d0f411066d18a2164f9d8b5069812277a8a440cb571d86e3f1
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A HumanLayer post arguing that most coding-agent failures are configuration problems rather than model problems, and walking through the configuration surface it calls the agent's harness: agent files, MCP servers, skills, sub-agents, hooks and back-pressure."
  author: ["Kyle"]
  datePublished: "2026-03-12"
  publisher: "HumanLayer"
---

The post's thesis is in its title: after a year of watching coding agents ignore instructions, run
dangerous commands and go in circles, the authors kept concluding that the problem was not the model
but its configuration. Smarter models will remove some failure modes, it argues, but will then be given
bigger problems and fail in new, unexpected ways, so the useful question is how to get the most out of
today's models. It summarizes this as "coding agent = AI model(s) + harness", where the harness is the
agent's configuration surface — skills, MCP servers, sub-agents, memory, AGENTS.md files and the like.

It says the term [[DefinedTerm/harness-engineering]] was coined by Viv, describes it as the practice of
leveraging these configuration points to improve a coding agent's output quality and reliability, and
positions it as a subset of [[DefinedTerm/context-engineering]] — the part
that uses harness configuration points to manage coding agents' context windows. The rest of the post
goes through each configuration surface in turn with HumanLayer's own practices.

## Key Points

- CLAUDE.md / AGENTS.md files (see [[DefinedTerm/claude-md]] and [[DefinedTerm/agents-md]]) are the first
  thing to customize: markdown files at the top of a repository that the harness injects into the
  agent's system prompt. The post restates its own earlier advice from
  [[BlogPosting/writing-a-good-claude-md]] — do not auto-generate the file, keep it concise and
  universally applicable, use progressive disclosure — and says HumanLayer's own CLAUDE.md is under 60
  lines.
- MCP servers are for tools. Their tool descriptions are injected into the system prompt, so too many
  tools push the agent toward the "dumb zone", and an untrusted server is a prompt-injection vector. Where
  an MCP server duplicates a CLI well represented in training data (GitHub, Docker, most databases), the
  authors found prompting the agent to use the CLI works better; they replaced the Linear MCP server with
  a small context-efficient CLI documented in their CLAUDE.md (see [[DefinedTerm/model-context-protocol]]).
- Skills are for reusable knowledge and tools through progressive disclosure: the agent gets specific
  instructions or tools only when it decides it needs them (see [[DefinedTerm/agent-skills]] and
  [[DefinedTerm/progressive-disclosure]]). The post warns that skill registries have been caught
  distributing malicious skills and advises reading a skill before installing it.
- Sub-agents are for context control, not for role-play: "frontend engineer" or "backend engineer"
  sub-agents did not work for the authors, whereas using sub-agents as a "context firewall" — the parent
  sees only the prompt it wrote and the condensed result — keeps the parent thread coherent across many
  context windows, which the authors tie to models performing worse at longer context lengths (see
  [[DefinedTerm/context-rot]]). They also use a cheaper model for sub-agents than for the parent session
  to control cost.
- Hooks are for control flow: user-defined scripts run at points in the agent's lifecycle, used for
  notifications, automatic approval or denial of tool calls, integrations and verification. Its example
  hook runs a formatter and type checks when Claude stops, stays silent on success, and returns exit code
  2 on failure so the harness makes the agent fix the errors (see [[DefinedTerm/agent-hooks]]).
- Back-pressure: the post states that the likelihood of solving a problem with a coding agent is strongly
  correlated with the agent's ability to verify its own work, calls its tests and verification
  mechanisms one of the highest-leverage things the team has built, and insists they be context-efficient
  (see [[DefinedTerm/backpressure]] and [[BlogPosting/context-efficient-backpressure-for-coding-agents]]).
- On post-training, it acknowledges that a model may perform better in the harness it was post-trained
  on, but argues this cuts both ways because models can be over-fitted to their harness, so it is not a
  reason to leave the harness uncustomized.

## Context

The recommendations come from HumanLayer's own experience over "dozens of projects and hundreds of agent
sessions", and the post closes with the team's own list of what did and did not work: start simple and
add configuration only when the agent actually fails, rather than designing an ideal harness upfront or
installing many skills and MCP servers "just in case". It presents itself as a companion to Viv's own
writing on harnesses, adding two levers it says he does not emphasize: hooks for deterministic control
flow and skills for progressive disclosure of knowledge. Related pages include
[[DefinedTerm/agent-harness]] and [[BlogPosting/advanced-context-engineering-for-coding-agents]].
