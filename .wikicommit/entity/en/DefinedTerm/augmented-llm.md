---
title: "Augmented LLM"
type: "schema:DefinedTerm"
lang: en
tags: [llm, agents, terminology]
sources:
  - type: url
    url: 'https://simonwillison.net/2024/Dec/20/building-effective-agents/'
    hash: sha256:18b0b6ac2ea34d146b6965fb5712a728a38e21351a665e839be4867f30c8b1a2
  - type: url
    url: 'https://www.anthropic.com/research/building-effective-agents'
    hash: sha256:611504eb30423330be060ed8f00e432a0adcb417f992b2cfb5cbf9ccd8d511bf
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
link post about their article. The definition available through that source is correspondingly
brief — an LLM with augmentations such as tools. The article he is reporting is held directly by this
page as well, and is read below.

## The Primary Account

The article Willison reports is [[BlogPosting/building-effective-agents]], which this page now also
holds directly, so the term can be read in the words that introduced it rather than only at one
remove.

There, the augmented LLM is presented as the **basic building block** of agentic systems: a model
enhanced with augmentations such as retrieval, tools and memory. What Anthropic emphasises about the
current generation of models is that they can use those capabilities actively rather than being
driven through them — generating their own search queries, selecting appropriate tools, and
determining what information to retain. The post's two implementation recommendations are to tailor
these capabilities to the specific use case, and to give the model an easy, well-documented interface
to them; [[DefinedTerm/model-context-protocol]] is named as one way to supply that interface.

Its place in the post's structure is what makes it a building block rather than one option among
several. Everything the post goes on to describe — prompt chaining, routing, parallelization,
orchestrator-workers, evaluator-optimizer, and the autonomous agent — is built on the assumption,
stated explicitly, that every LLM call from that point onwards has these augmented capabilities
available. So the augmented LLM is not the simplest item in a list of architectures; it is the unit
the rest of the list is composed from.

That also sharpens the boundary Willison values. Anthropic groups workflows and agents together as
agentic systems and separates them by who directs the process — predefined code paths in a workflow,
the model itself in an agent (see [[DefinedTerm/ai-agent]]). Reading the augmented LLM as sitting below
that split — a single call with capabilities attached, not yet a system in which anything is being
orchestrated — is this page's own inference from its position as the building block; the post places it
before the patterns without placing it against the split itself.

## Related Terms

- [[DefinedTerm/tool-use-design-pattern]] — the mechanism the augmentation usually consists of
- [[DefinedTerm/ai-coding-agent]]
- [[DefinedTerm/sub-agent-architecture]]
