---
title: "Designing agentic loops"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, agent-tooling, sandboxing]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Sep/30/designing-agentic-loops/'
    hash: sha256:616bc39546fd4aab969e3a8ec0a6fa01330405714c063a028ab4419f84132964
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A post naming 'designing agentic loops' as a distinct skill: reducing a problem to a clear goal plus tools an agent can iterate against, then deciding how to run that loop safely and what credentials to expose to it."
  author: ["Simon Willison"]
  datePublished: "2025-09-30"
---

The post's argument starts from a particular way of seeing coding agents: as brute-force tools for
finding solutions to coding problems. On that view, a problem that can be reduced to a clear goal
plus a set of tools that iterate towards it is a problem an agent can often force its way through —
and the skill worth developing, which the post names **designing agentic loops**, is the careful
design of those tools and that loop. It rests the framing on the author's own preferred definition
of an [[DefinedTerm/ai-agent]] as something that runs tools in a loop to achieve a goal.

Most of the post's length goes to the obstacle this framing runs into. Brute force needs the agent
to run without stopping for approval at every step, and the author argues that the per-command
approval prompts agents default to, while safer, dramatically reduce their effectiveness at solving
problems this way. Removing them — what the post calls YOLO mode — is presented as both genuinely
dangerous and key to getting the most productive results, and the post works through the three ways
of living with that tension: a sandbox, someone else's computer, or accepting the risk.

The remainder is practical. On tools, the post argues that shell commands usually beat
[[DefinedTerm/model-context-protocol]] for this purpose, and that a short worked example in an
[[DefinedTerm/agents-md]]-style file is usually enough for an agent to generalise from. On
credentials, it recommends test or staging environments and hard budget limits. It closes by
characterising the problems worth this treatment as those with clear success criteria where finding
a good solution involves tedious trial and error, and names automated tests as the common factor
across its examples.

## Key Points
- Coding agents can be thought of as brute-force tools for finding solutions to coding problems: a
  problem reducible to a clear goal plus iterating tools can often be forced to a solution.
- Designing agentic loops is proposed as a critical new skill, and the post is explicit that it is
  naming the skill in the hope that a clear name makes it easier to discuss.
- The author's working definition of an agent — something that runs tools in a loop to achieve a
  goal — is what makes tool and loop design the place where skill is exercised.
- Per-command approval prompts are the default counter to agent danger, and they dramatically
  reduce an agent's effectiveness at brute-force problem solving.
- Three risks are named for unattended YOLO mode: bad shell commands damaging things you care
  about, exfiltration of files or secrets visible to the agent, and use of your machine as a proxy
  to attack another target.
- Three responses are offered: run in a secure sandbox, use someone else's computer, or take the
  risk and try to avoid exposing the agent to malicious instructions — and the author states that
  most people choose the third.
- Running on someone else's computer is the author's own favourite, with GitHub Codespaces named as
  his preferred instance of it; he bounds the worst case there as checked-out code being exfiltrated
  or bad code being pushed to the attached repository.
- Docker or Apple's container tool is judged a reasonable risk for most people despite the existence
  of container escapes — stated as the author's own risk judgment, not a security guarantee.
- Coding agents implement their own sandboxing, but the author reports not having seen documentation
  of it convincing enough to trust — his own assessment rather than a tested finding.
- The post quotes Anthropic's own Claude Code documentation on "Safe YOLO mode", which recommends
  running `--dangerously-skip-permissions` in a container without internet access; that recommendation
  is the vendor's, relayed here, not the post's own finding.
- Restricting an agent's internet access to a list of trusted hosts is presented as a good way to
  stop exfiltration attacks from stealing private source code.
- Shell commands are usually a more productive way to think about an agent's tools than MCP, because
  coding agents are good at running shell commands.
- A single worked example in an `AGENTS.md`-style file is often enough for an agent to generalise —
  the author's illustration is one screenshot command from which the agent inferred how to vary the
  URL and filename.
- Naming a well-known tool ("use playwright python", "use ffmpeg") is usually sufficient, because an
  agent running in a loop can recover from its own early mistakes.
- Credentials should be scoped to test or staging environments where damage is contained, and any
  credential that can spend money should carry a tight budget limit.
- The author's illustration of scoped credentials is a dedicated Fly.io organization with a $5 budget
  and an API key limited to it, created for a single cold-start investigation; he reports the
  investigation's results were not useful enough to describe.
- The pattern suits problems with clear success criteria where a good solution needs tedious trial
  and error — the signal offered is catching yourself thinking you will have to try a lot of variations.
- Four example problem shapes are given: debugging a failing test, performance optimization such as
  benchmarking an index, upgrading dependencies, and shrinking container images.
- A good, cleanly passing test suite is named as the common factor that amplifies the value of coding
  agents across all of those examples.

## Context
The post belongs to the author's ongoing series on his own use of LLMs and is explicitly presented
as an early attempt at naming something rather than a settled account: it closes by observing that
the area is very fresh and that there is much more to figure out. Its evidence is the author's own
practice — the Fly.io investigation, the screenshot tooling, his preference for disposable cloud
environments — rather than measurement, and its security recommendations are framed as personal risk
judgments, including the concession that most people take the unmitigated option. An update appended
after publication points at Anthropic's own documentation for the same practice, which the post treats
as corroboration from the vendor rather than as its own evidence.
