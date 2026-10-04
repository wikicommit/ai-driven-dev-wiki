---
title: "Prüfen Coding-Agents Lizenzen?"
type: "schema:BlogPosting"
lang: en
tags: [open-source-licensing, prompt-injection, harness-engineering, supply-chain]
sources:
  - type: url
    url: 'https://www.codecentric.de/wissens-hub/blog/pruefen-coding-agents-lizenzen'
    hash: sha256:c38afd754438229f1c0570cd206b7ef55a531a9abaac3e23485f1b8426b6e0ba
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A German-language codecentric blog post asking whether coding agents check a library's license before using it, concluding that markers placed in a library do not reach the agent, that a runtime notice that does is effectively prompt injection, and that license checking belongs to the consumer and their harness."
  author: ["Johannes Barop"]
  datePublished: "2026-07-28"
  publisher: "codecentric"
---

This post on codecentric's German-language blog ("Do coding agents check licenses?"), by Johannes Barop, starts from an incident in early 2026 in which, it says, a well-known Java library tried to turn coding agents against their own users through prompt injection, because its maintainers were critical of AI tools and did not want the library used by AI agents. Wondering how a maintainer could add a clause prohibiting use by AI agents to a license such as the GPL or MIT, the author ran into a prior question: do coding agents check a library's license at all before using it?

The post reports the author's own experiments with what a library can do to get its maintainers' position across to an agent, and with what a consumer can instruct their agent to do. Its answer is that the library side can achieve very little, that the one channel that works is the same one prompt injection uses, and that responsibility lies with the consumer — ideally enforced in the [[DefinedTerm/agent-harness]] rather than left to each user.

## Key Points

- For a standard task against a well-known library, the post says, the model behind the agent supplies the solution directly from its training data without the agent inspecting the library, so a license shipped in the package never reaches the agent.
- In the library from the introduction, the maintainers' position on AI is stated not in the license but in a separate file in the source repository on GitHub that reaches neither the package nor the registry metadata, so even an agent that checked the license would not find the prohibition.
- The author tried variants ranging from a license addendum through machine-readable standards to a code marker; none reached the agent, because it does not analyse the library. A license clause also prohibiting use as training data would not change this either, the post argues, since the library's usage already appears in many other projects, tutorials and forum posts that themselves flow into training data.
- A runtime notice reliably reached the agent: a static initializer in a central API class writes the notice to `stderr` when the library loads, and the agent has to read the `stderr` output of its tool calls to plan its next step.
- The post calls that notice the same basic technique as the prompt-injection incident (see [[DefinedTerm/prompt-injection]]): text placed in a channel the agent must read rather than somewhere it actively looks. It notes that the notice avoids instructions and claims about consequences, unlike the incident, but that the line stays fluid because informative wording can become an instruction with little effort.
- The license nonetheless remains the right place for such a clause, the author argues, because licenses exist to state terms of use and that is where a consumer can have their agent look.
- With a short instruction — "Before adding or updating any library, check its license." — the agent, tested on the same library with an AI-prohibition clause the author had added to its license, found the license, recognised the clause and described the problem to the user. The author expects reliability to depend on the project and dependency ecosystem, suggests that instructions spelling out a search strategy probably improve the hit rate and speed, and proposes a dedicated skill so that users need not each reinvent that strategy.
- License compliance, the post says, was always the consumer's responsibility rather than the library's, and coding agents do not change that; the consumer can configure the agent to do the check they would previously have done themselves.
- The answer is split across three actors as of 2026: maintainers, who must make the license findable in the repository and who may resort to a runtime notice that is in effect a prompt injection; consumers, who must respect the license terms; and the harness, which the author takes to include not only the coding agent but also the workflow around it, such as a CI pipeline before every merge.
- In [[DefinedTerm/vibe-coding]] mode, where the user sets only a goal and does not check each intermediate step, a new dependency easily goes unnoticed while tests stay green, so the post argues that a license check must be anchored technically in the harness, for instance as an automatic step before every merge.
- That check should cover more than an AI-prohibition clause: licenses have always governed which other code a library may be combined with and what it may be used for, two individually unremarkable licenses can form an impermissible combination in one project (for example GPL code next to proprietary code), and some licenses restrict commercial use.

## Context

The post is based on the author's own experiments with a single library and does not report measured rates; it says explicitly that how reliably an agent finds a license probably depends on the project. Its closing position is that an agent can take over the license check, but the responsibility stays with the team that deploys it — which places the argument alongside writing on [[DefinedTerm/harness-engineering]] that treats checks around the agent, rather than the agent's own diligence, as the point of control.
