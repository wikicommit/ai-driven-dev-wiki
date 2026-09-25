---
title: "Le développement logiciel à l’ère des agents IA"
type: "schema:BlogPosting"
lang: en
tags: [coding-agents, team-organization]
sources:
  - type: url
    url: 'https://blog.octo.com/le-developpement-logiciel-a-l''ere-des-agents-ia'
    hash: sha256:5f3659e3312d232fa458c15b3683f0b90d22b6de8edc980b38fc9be979fbd6a5
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A French-language post on blog.octo.com, dated 22 January 2026, arguing that generative-AI agents turn the developer's job from writing code into orchestrating several agents in parallel. It describes an augmented developer working in pairs, smaller teams with faster delivery, and a bottleneck that moves from technical execution to the quality of business requirements."
  author: ["Bruno Boucard"]
  datePublished: "2026-01-22"
---

*Le développement logiciel à l’ère des agents IA* ("Software development in the age of AI agents")
presents the rise of generative-AI agents as an organizational transformation rather than a change of
tools. Its central claim is that the developer no longer mainly writes code but orchestrates a
production in which several specialised agents work in parallel, becoming a "conductor" who steers,
coordinates and guides them. The post calls this role the [[DefinedTerm/augmented-developer]].

From that premise it draws consequences for how teams are organized: recruitment slows and favours
profiles able to take on the augmented role, teams shrink while delivery cadences accelerate sharply,
and a pair of augmented developers — rather than a single orchestrator — emerges as the basic
organizational unit. The limiting factor, it argues, is no longer technical but functional: the quality
of the business needs handed to the agents.

The post then applies the argument to offshore development, Low Code / No Code, the CI/CD chain and the
place of junior developers, and ends by presenting the resulting organization as one that makes a
fully assumed "product first" approach possible.

## Key Points

- Recent agents let a team state an application's invariants explicitly in configuration artefacts,
  generally Markdown files, describing target architecture, testing and mocking strategies and code
  generation conventions, alongside more functional files stating known business rules.
- These tools make the generation plan explicit — task sequencing, each agent's area of
  responsibility, extension points and produced artefacts — so the orchestrating developer sees the
  *what*, *where* and *how* of generation.
- Planning adds an up-front time cost, but lets work be parallelised across agent instances, which the
  post says improves overall cycle time and predictability.
- Development becomes a continuous flow of parallel productions, which Kanban-style tools can make
  visible while limiting work in progress and cognitive saturation; an agent is a development resource
  whose cost, notably in tokens, should be compared with a human developer's against the value produced.
- A single orchestrating developer is fragile because of the bus factor; the post presents the pair of
  augmented developers, working in a spirit of mentorship (*compagnonnage*), as the stable minimal unit.
- The post claims that such pairs, with strong business understanding, can produce in a day what a
  team of five previously produced over several months — an assertion made without supporting data.
- The bottleneck moves to business requirements: user stories are often poorly qualified, rarely
  INVEST-compliant and seldom illustrated by concrete examples, while agents excel when expectations are
  clear, contextualised and example-backed. Qualifying business examples remains human work, and
  practices such as Example Mapping supply the raw material for prompts.
- The post calls persisting with low-cost offshore development a strategic error, and argues that AI
  should instead bring the business closer to the teams that build the product.
- It argues that code-generating agents make Low Code / No Code much less relevant beyond simple
  prototypes, since they offer tailored code with the control, scalability and maintainability of
  general-purpose languages.
- Faster production requires a fully automated CI/CD chain into which AI is integrated to observe
  flows, analyse weak signals, qualify incidents and produce feedback, moving delivery towards the
  continuous flow described in *Team Topologies*.
- Junior developers are not excluded, but need a redesigned learning path — pair programming with a
  senior, hands-on adjustments of generated code, and deliberate practice such as code katas.
- The key profile the post names is a senior developer with strong business maturity, at the crossroads
  of Tech Lead and Product Owner.

## Context

The post is an argument from its author's perspective rather than a report of measured results; its
productivity and cost claims are stated without data. It situates the product-first outcome in the
promise of Marty Cagan's *Inspired* and in the Product Trio of UX Designer, Product Manager and Tech,
and names Example Mapping, DDD and BDD as the practices that become essential once requirements are the
constraint.

Related posts in this wiki:
[[BlogPosting/organizing-a-development-team-in-the-age-of-ai-part-ii-2]] and
[[BlogPosting/organizing-a-development-team-in-the-age-of-ai-part-iii]].
