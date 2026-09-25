---
title: "Tool Namespacing"
type: "schema:DefinedTerm"
lang: en
tags: [tool-use, agent-tooling, agent-architecture]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/writing-tools-for-agents'
    hash: sha256:7541e4e46d675b2aed1175d9291d45d75f493ae908aea2afc77b29c615a324ea
  - type: url
    url: 'https://platform.openai.com/docs/guides/function-calling'
    hash: sha256:837fddfb4f47440271a02bb4e3bf476c552ccbfc1b962b602a0217dc5bf68f47
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Grouping related agent tools under common name prefixes — by service, by resource, or both — so that an agent with access to many overlapping tools can tell which one to reach for. Anthropic reports that the choice between prefix- and suffix-based schemes had non-trivial effects on its tool-use evaluations and varied by model."
---

Tool namespacing is the practice of grouping related tools under common prefixes so that the
boundaries between them are legible to an agent choosing among them. It is set out under that name in
[[BlogPosting/writing-effective-tools-for-agents]], which motivates it by the situation an agent is
increasingly in: access to dozens of [[DefinedTerm/model-context-protocol]] servers and hundreds of
tools, including tools written by other developers, where overlapping function or vague purpose leaves
the agent unsure which to call. Some MCP clients are reported to apply namespacing by default.

## Usage

The post describes two axes, which can be combined. Tools may be namespaced **by service**, so that
searching in one product and searching in another carry distinct prefixes rather than competing as two
tools both called "search"; and **by resource**, so that searching projects and searching users within
the same service are separated in turn. The examples given are service-level names of the form
`asana_search` and `jira_search`, and resource-level names of the form `asana_projects_search` and
`asana_users_search`.

The choice of scheme is presented as an empirical question rather than a convention. The authors report
that selecting between prefix- and suffix-based namespacing had non-trivial effects on their own
tool-use evaluations, that the effects vary by model, and they recommend choosing a naming scheme
according to one's own evaluations rather than adopting a rule.

OpenAI's function-calling guide (see [[DefinedTerm/function-calling]]) supports the practice as an
API feature rather than a naming convention: related tools can be grouped into namespaces by domain, with
`crm`, `billing` and `shipping` as its examples. It gives the same motivation — namespaces are
especially useful when the model must choose between tools serving different systems or purposes, such
as one search tool for a CRM and another for a support ticketing system. Where namespaced tools are
deferred with [[DefinedTerm/tool-search]], the guide advises keeping the namespace description concise
and putting detailed guidance in each function's description, since the namespace helps the model
choose what to load and the function description helps it use the loaded tool correctly.

The post places namespacing alongside a second, related discipline: selectively implementing tools whose
names reflect natural subdivisions of tasks. It is that second practice the post credits with
simultaneously reducing the number of tools and tool descriptions loaded into the agent's context and
offloading agentic computation from that context back into the tool calls themselves.

## When It Applies

It applies where an agent has enough tools available that selection itself becomes a failure point. The
failure modes the post names are calling the wrong tool, calling the right tool with the wrong
parameters, calling too few tools, and processing tool responses incorrectly. What the post credits
namespacing itself with is helping delineate boundaries and helping agents select the right tools at the
right time; it attaches the broader claim about reducing an agent's overall risk of mistakes to the
neighbouring practice of naming tools after natural subdivisions of tasks.

It assumes the tools are yours to name, or at least that the client can rewrite names on the way
through. The post notes separately that MCP clients sometimes apply namespacing by default, and that an
agent's tools may include those written by other developers. It also assumes names carry meaning for the model, which is the same assumption behind the
post's separate advice on prompt-engineering tool descriptions and on naming parameters unambiguously.

The technique is not presented as sufficient on its own. In the same post it is one of five principles,
and the one preceding it — building a few thoughtful, consolidated tools rather than wrapping every API
endpoint — addresses the same underlying problem from the other end, by not creating the overlapping
tools in the first place.

How well-established it is: the naming advice is one vendor's engineering guidance, drawn from optimizing its own
internal tools against its own evaluations. The direction of the advice is stated as a finding; the
specific choice between prefix and suffix is explicitly left to the reader's own measurement. OpenAI's function-calling
guide separately offers namespaces as a first-class API feature for grouping tools by domain.

## Related Terms

- [[DefinedTerm/tool-use-design-pattern]] — the broader pattern this is a design discipline within
- [[DefinedTerm/model-context-protocol]] — the protocol whose tool sprawl motivates the practice
- [[DefinedTerm/context-engineering]] — the concern that tool names and descriptions occupy context
- [[DefinedTerm/function-calling]] — the mechanism through which namespaced tools are offered to a model
- [[DefinedTerm/tool-search]] — deferring namespaced tools until the model needs them
