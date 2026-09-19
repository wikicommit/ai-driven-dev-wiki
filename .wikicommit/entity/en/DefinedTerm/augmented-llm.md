---
title: "Augmented LLM"
type: "schema:DefinedTerm"
lang: en
tags: [llm, agents, terminology]
sources:
  - type: url
    url: 'https://simonwillison.net/2024/Dec/20/building-effective-agents/'
    hash: sha256:18b0b6ac2ea34d146b6965fb5712a728a38e21351a665e839be4867f30c8b1a2
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A name for an LLM extended with augmentations such as tools — the thing on its own, rather than a system that orchestrates several LLM calls. Simon Willison reports the term from an Anthropic piece on building agentic systems and endorses it as the word that was missing for something people had been calling an agent."
---

An augmented LLM is a large language model equipped with augmentations such as tools. Simon
Willison reports the term from an Anthropic article about building agentic systems and singles it
out as one he really likes, on the grounds that he has seen people use "agents" for just this —
a model with tools attached — which never felt right to him. The term's value on his account is
therefore boundary-drawing: it gives the simplest case its own name, so that "agent" does not
have to cover it.

## Usage

What Willison praises the article for is defining its terms at all: his standing complaint about
"agents" is that the word has many potential definitions while most people using it assume
everyone shares the one they picked, and he credits the article with bucking that trend from the
start. As he reports it, the article treats "agentic systems" as a parent term and then
distinguishes "workflows" — systems where multiple LLMs are orchestrated together using
pre-defined patterns — from "agents", where the LLMs dynamically direct their own processes and
tool usage. The augmented LLM is a further term he singles out from the same article, and it names
a different kind of thing from either: a single LLM with augmentations such as tools, rather than
several LLMs arranged into a system.

The distinction matters most where the word "agent" is being claimed. Willison's account of the
article's own advice points the same way — that when building applications with LLMs the
recommendation is to find the simplest solution possible and only increase complexity when needed,
which might mean not building agentic systems at all, and to avoid investing in complex agent
frameworks before exhausting direct API access and simple code. Naming the simplest configuration
is what makes it possible to say that a given system is only that.

Nothing here is Willison's own coinage: he is reporting and endorsing someone else's term, in a
link post about their article. The definition available through this source is correspondingly
brief — an LLM with augmentations such as tools — and the article that introduced it is not itself
among this page's sources.

## Related Terms

- [[DefinedTerm/tool-use-design-pattern]] — the mechanism the augmentation usually consists of
- [[DefinedTerm/ai-coding-agent]]
- [[DefinedTerm/sub-agent-architecture]]
