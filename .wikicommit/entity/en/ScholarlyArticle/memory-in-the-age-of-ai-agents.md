---
title: "Memory in the Age of AI Agents: A Survey — Forms, Functions and Dynamics"
type: "schema:ScholarlyArticle"
lang: en
tags: [agent-architecture, context-engineering, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.13564'
    hash: sha256:bf1d2af2865778054a49d2de7020b127bba914eb01936a21e9a029f00a99cd6e
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A large multi-institution survey of agent memory, written against a field it describes as fragmented by loosely defined terminology. It replaces the long/short-term split with three lenses — forms (token-level, parametric, latent), functions (factual, experiential, working), and dynamics — and explicitly delimits agent memory from LLM memory, RAG, and context engineering."
  datePublished: "2025-12"
---

"Memory in the Age of AI Agents" is a survey with a very large author list — core contributors listed alphabetically, a project organizer, and several core supervisors — spanning the National University of Singapore, Renmin University of China, Fudan University, Peking University, Nanyang Technological University, Tongji University, UC San Diego, HKUST (Guangzhou), Griffith University, Georgia Tech, OPPO, and Oxford University.

Its motivation is definitional disorder rather than a technical gap. The survey states that as research on agent memory has expanded, "the field has also become increasingly fragmented": works under the same umbrella "differ substantially in their motivations, implementations, assumptions, and evaluation protocols, while the proliferation of loosely defined memory terminologies has further obscured conceptual clarity." Its verdict on the vocabulary in common use is direct — "traditional taxonomies such as long/short-term memory have proven insufficient to capture the diversity and dynamics of contemporary agent memory systems."

Its first move is therefore to draw boundaries: it delineates the scope of agent memory and distinguishes it from LLM memory, [[DefinedTerm/retrieval-augmented-generation]], and [[DefinedTerm/context-engineering]] — three neighbours whose conflation with agent memory the survey treats as part of the problem.

## Key Contributions

The survey examines agent memory through three lenses, which are its organising contribution.

- **Forms — what carries memory.** Three dominant realizations: **token-level** memory, stored as discrete explicit units; **parametric** memory, held in weights; and **latent** memory, in intermediate representations. The survey describes token-level memory as the most common form and the one with the largest body of work, and notes the property that follows from its explicitness: because the units are visible, it is "typically transparent, easy to edit, and straightforward to interpret, making it a natural layer for retrieval, routing, conflict handling, and coordination with parametric and latent memory."
- **Functions — why agents need memory.** Here the survey deliberately moves "beyond coarse temporal categorizations" and proposes distinguishing **factual**, **experiential**, and **working** memory. The point of the substitution is that what a memory is *for* cuts differently from how long it lasts.
- **Dynamics — how memory operates and evolves.** How memory is formed, evolved, and retrieved over time as an agent interacts with its environment.

It additionally compiles a summary of representative benchmarks and open-source memory frameworks, and closes with a section on positions and emerging research frontiers.

## Notes

The taxonomy's practical value here is that it separates axes the vocabulary in this wiki tends to collapse. [[DefinedTerm/agentic-memory]] as the vendor and practitioner accounts describe it — writing notes to files outside the context window and reading them back — is one cell of this map: token-level in form, mostly experiential or factual in function. Parametric and latent memory do not appear in those accounts at all, because a coding agent's operator cannot manipulate them; and the survey's insistence that agent memory is distinct from retrieval-augmented generation and from context engineering is the same boundary practitioners blur when they treat "memory" as whatever is not in the current window.

This is a literature survey rather than new measurement, and its subject is agents in general rather than coding agents, so its claims belong to the works it reviews. The material summarised here comes from its abstract, introduction, and section structure.
