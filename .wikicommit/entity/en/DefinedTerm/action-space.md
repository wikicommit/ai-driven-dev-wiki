---
title: "Action-Space"
type: "schema:DefinedTerm"
lang: en
tags: [agents, governance, agent-safety, human-oversight]
sources:
  - type: url
    url: 'https://www.imda.gov.sg/-/media/imda/files/about/emerging-tech-and-research/artificial-intelligence/mgf-for-agentic-ai.pdf'
    hash: sha256:ade20c2fa2aedf4f9ea3efe129e8b2ed3cc7823b414e766050586231d956645e
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The range of actions an agent can take, determined by the tools it is allowed to use and its permissions on them - held distinct from autonomy, which is how far the agent decides for itself how to act."
---

Action-space is the range of actions an agent can take, including the transactions it can execute,
determined by the tools it is allowed to use and its permissions on those tools. The term is also
given as authority or capabilities. [[TechArticle/model-ai-governance-framework-for-agentic-ai]]
presents it as one of two concepts worth distinguishing when asking what an agent can do, the other
being autonomy: the degree to which an agent can decide how to act towards a goal, such as by
defining the steps to be taken, determined by its instructions and the level of human involvement.

## Usage

An agent's action-space depends mainly on the systems its tools reach — sandboxed tools that cannot
affect anything else, internal systems such as the organisation's own databases, or external
systems reached through third-party APIs — and on whether it can only read from those systems or
also write to and modify them. A computer use agent is described as an emerging modality that
expands the action-space sharply, because access to a computer and browser lets it take any action
a human could take with them (scrolling, clicking, typing) without relying on specifically defined
tools and APIs.

Autonomy, the other axis, turns on how prescriptive the instructions are — a detailed SOP versus an
instruction to use the agent's own judgment — and on where the deployment sits on a spectrum of
human involvement running from *agent proposes, human operates* through *agent and human
collaborate* and *agent operates, human approves* to *agent operates, human observes*. The two axes
are treated as independent: the framework illustrates them with a software engineering agent that
can search and read any file to diagnose issues but has no write access (more autonomy, smaller
action-space) set against one that can browse the web and modify files but only with human approval
at each step or under a fixed SOP (less autonomy, larger action-space).

Separating the axes matters for risk assessment, where they enter on different sides: the scope of
an agent's actions and their reversibility are listed among the factors affecting the *impact* of a
failure, while the agent's level of autonomy is listed among the factors affecting its
*likelihood*, on the stated reasoning that higher autonomy produces more unpredictability.

## Related Terms

[[DefinedTerm/agentic-autonomy-levels]], [[DefinedTerm/supervised-agency-spectrum]],
[[DefinedTerm/human-in-the-loop]], [[DefinedTerm/computer-use]], [[DefinedTerm/sandboxing]]
