---
title: "agent-computer interface"
type: "schema:DefinedTerm"
lang: en
tags: [tool-design, agent-architecture, terminology]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/building-effective-agents'
    hash: sha256:89d6d2e67b90631137ed1aba80dbebb0264d98646e0db9850e22d6a6c80c67cf
  - type: url
    url: 'https://www.anthropic.com/engineering/multi-agent-research-system'
    hash: sha256:f9af507dbe72a9650f1c11cf6ae2aa13e7f9c2f6c3a7436129197c31ddb3a3bc
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The surface through which a model perceives and operates its tools — their formats, names, parameters and documentation — held to deserve as much design effort as a human-computer interface would."
  termCode: "ACI"
  inDefinedTermSet: ""
---

The agent-computer interface — abbreviated ACI — is the surface through which a model perceives and operates its tools: how actions are specified, what parameters are called, how formats are shaped, and what the documentation says. [[TechArticle/building-effective-agents]] introduces it by analogy: "think about how much effort goes into human-computer interfaces (HCI), and plan to invest just as much effort in creating good *agent*-computer interfaces (ACI)." Careful ACI design is one of that post's three closing principles for building agents.

## Usage

**Format choice is not cosmetic.** That post's example is that a file edit can be specified as a diff or as a full rewrite, and structured output can be returned in markdown or JSON — differences a software engineer would call lossless conversions. But some formats are much harder for a model to write: a diff requires knowing how many lines change in the chunk header *before* the new code is written, and code inside JSON requires escaping newlines and quotes.

Three rules follow for choosing a format: give the model enough tokens to think before it writes itself into a corner; keep the format close to what the model has seen naturally occurring in text on the internet; and ensure there is no formatting overhead such as keeping an accurate count of thousands of lines or string-escaping code.

**Four practices** are given for the interface itself. *Put yourself in the model's shoes* — if using the tool would take careful thought from you based on its description and parameters, it will for the model too, and a good tool definition often includes example usage, edge cases, input format requirements, and clear boundaries from other tools. *Write parameter names and descriptions like a great docstring for a junior developer*, which matters most when many similar tools are in play. *Test how the model actually uses the tool*, running many example inputs to see what mistakes it makes and iterating. And *poka-yoke the tools* — change the arguments so mistakes are harder to make.

**The reported payoff** is that while building an agent for [[Dataset/swe-bench]], the team spent more time optimising tools than the overall prompt. The concrete case given: the model made mistakes with tools using relative filepaths once the agent had moved out of the root directory, and changing the tool to always require absolute filepaths made it use the method flawlessly.

### Tools as a failure surface in production

[[TechArticle/how-we-built-our-multi-agent-research-system]] restates the principle in the same terms — "agent-tool interfaces are as critical as human-computer interfaces" — and adds what goes wrong at scale. Choosing the wrong tool is often fatal rather than merely inefficient: "an agent searching the web for context that only exists in Slack is doomed from the start." [[DefinedTerm/model-context-protocol]] servers compound the problem, since agents then encounter unseen tools whose descriptions vary wildly in quality, and a bad description "can send agents down completely wrong paths." Its answer was explicit selection heuristics in the prompt — examine all available tools first, match tool usage to user intent, use web search for broad external exploration, prefer specialised tools over generic ones — plus a requirement that each tool have a distinct purpose and a clear description.

The same post reports automating the improvement itself. A **tool-testing agent** was given a flawed MCP tool, attempted to use it, and rewrote the tool description to avoid the failures it hit; testing the tool dozens of times surfaced key nuances and bugs. The reported result was a 40% decrease in task completion time for later agents using the new description, because they avoided most of the mistakes.

## Related Terms

The ACI is the part of an [[DefinedTerm/agent-harness]] the model actually sees, and designing it well is the same discipline [[DefinedTerm/context-engineering]] applies to what the model reads. It sits alongside simplicity and transparency in that post's three principles for [[DefinedTerm/agentic-system]] design.
