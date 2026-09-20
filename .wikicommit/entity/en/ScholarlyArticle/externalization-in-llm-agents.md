---
title: "Externalization in LLM Agents: A Unified Review of Memory, Skills, Protocols and Harness Engineering"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, agent-architecture, surveys, memory, agent-tooling]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.08224'
    hash: sha256:3d6692b679c69f74f38b4515cebbbd196a2a08273d14166866ba9d19bf479ea8
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A systems-level review arguing that progress in LLM agents comes increasingly from externalising cognitive burdens into memory stores, reusable skills and interaction protocols, coordinated by a harness. It traces a progression from weights to context to harness and sets out six analytical dimensions of harness design."
  author: ["Chenyu Zhou", "Huacan Chai", "Wenteng Chen", "Zihan Guo", "Rong Shan", "Yuanyi Song", "Tianyi Xu", "Yingxuan Yang", "Aofan Yu", "Weiming Zhang", "Congming Zheng", "Jiachen Zhu", "Zeyu Zheng", "Zhuosheng Zhang", "Xingyu Lou", "Changwang Zhang", "Zhihui Fu", "Jun Wang", "Weiwen Liu", "Jianghao Lin", "Weinan Zhang"]
  datePublished: "2026-04-10"
  abstract: "LLM agents are increasingly built less by changing model weights than by reorganizing the runtime around them. Capabilities that earlier systems expected the model to recover internally are now externalized into memory stores, reusable skills, interaction protocols, and the surrounding harness that makes these modules reliable in practice. Drawing on the idea of cognitive artifacts, the review argues that agent infrastructure matters not merely because it adds auxiliary components, but because it transforms hard cognitive burdens into forms the model can solve more reliably: memory externalizes state across time, skills externalize procedural expertise, protocols externalize interaction structure, and harness engineering coordinates them into governed execution."
---

This review argues that the most consequential recent advances in LLM agents are not changes to
models but changes to the runtime around them, and it supplies a single concept to explain why the
separate literatures on memory, skills, protocols and harnesses are converging. That concept is
**externalization**: the progressive relocation of cognitive burdens from the model's internal
computation into persistent, inspectable, reusable external structures.

The theoretical anchor is Donald Norman's account of cognitive artifacts, from which the authors take
the claim that an external aid does not simply amplify an unchanged internal ability but transforms
the task itself. Their recurring illustrations are Norman's: a shopping list does not expand
biological memory capacity, it converts a difficult recall problem into a recognition problem; a map
does not make navigation stronger, it converts hidden spatial relations into visible structure. The
paper extends this into a deliberate parallel between the arc of human cognitive externalization —
language, writing, printing, digital computation — and the arc it traces for LLM agents.

The review's structure follows three externalization dimensions plus the layer that unifies them.
**Memory** externalizes state across time, converting recall into recognition. **Skills** externalize
procedural expertise, converting improvised generation into composition. **Protocols** externalize
interaction structure, converting ad hoc coordination into governed contract. The **harness** is not
a fourth kind of externalization but the runtime environment within which the three operate and
interact.

## Key Points

- The paper frames recent history as a progressive outward movement across three layers — Weights,
  Context, and Harness — and is careful that these are layered rather than mutually exclusive:
  weights remain important even in the most infrastructure-heavy systems, but each stage changes
  where developers place the system's mutable intelligence and therefore where they invest
  engineering effort.
- It states the central limitation of weight-space capability as a governance problem rather than a
  capability one: parametric knowledge is difficult to selectively update, compose and govern, and
  auditing why a model behaved a certain way is hard because the relevant knowledge is distributed
  across billions of parameters rather than encoded as inspectable modules.
- It maps three recurrent mismatches of an unaided model onto the three externalization dimensions: a
  **continuity** problem (finite context and weak session memory) that memory addresses, a
  **variance** problem (long procedures rederived rather than executed consistently) that skills
  address, and a **coordination** problem (brittle interaction with tools and collaborators under
  free-form prompting) that protocols address.
- It reads the context-centric stage through the same Norman lens: the difficult question "does the
  model know fact X?" is converted into the easier one "given that fact X has been placed in context,
  can the model use it?" — and notes this mirrors the recall-to-recognition shift associated with
  writing in the human arc.
- It argues that expanding context windows does not dissolve the underlying tension, citing the
  "lost in the middle" finding that models attend unevenly across long inputs, and observing that
  context is also ephemeral: unless state is externalized elsewhere, every new session begins with
  partial amnesia.
- On the harness it makes a definitional claim rather than an implementational one: a harness is not
  an implementation convenience layered on a capable model but the **designed cognitive environment**
  within which externalized modules become jointly effective. Agency, on this account, is not located
  in the model alone but emerges from the coupling of the model with the environment that organises
  its cognition into action.
- It notes the term is still consolidating and presents its own characterisation as a synthesis of
  recurring patterns in current systems rather than a closed definition.
- It decomposes harness design into six analytical dimensions grouped under three operational
  surfaces — Permission, Control and Observability: agent loop and control flow, sandboxing and
  execution isolation, human oversight and approval gates, observability and structured feedback,
  configuration and policy encoding, and context budget management. None of the six is itself a form
  of externalization; they are the coordinative infrastructure that makes the three modules cohere.
- On control it argues that termination, recursion and cost limits are not secondary safety measures
  but definitional: they set the operational envelope within which reasoning unfolds, and a well-tuned
  loop makes an agent more reliable not by making the model smarter but by bounding the space of
  possible execution paths.
- It makes the same move for sandboxing, arguing an execution boundary is not merely a security fence
  but a **cognitive boundary** that simplifies the operating environment by removing irrelevant state
  and restricting dangerous actions — serving the same representational function as other forms of
  externalization.
- It treats autonomy as a configurable parameter of the harness rather than a binary property of the
  agent, adjustable per task, per tool and per organisational policy, and describes three common
  oversight patterns: pre-execution approval, post-execution review, and escalation triggers, with
  hook systems generalising the pattern by attaching arbitrary logic to lifecycle events.
- It argues observability is the mechanism by which a harness learns from its own operation, not an
  auxiliary convenience: without structured traces the feedback loops that connect execution outcomes
  back to the modules that produced them cannot operate, and the harness remains a static scaffold
  rather than an adaptive system.
- It frames permissions and policies as **externalized governance** — constraints that would
  otherwise be embedded in prompts or enforced by post-hoc filtering are instead declarative rules the
  harness enforces at runtime, stratified across user, project and organisation scopes so that the
  same base agent can operate under different policy regimes without changing the model or its
  skill artifacts.
- It treats context budget as a harness-level coordination problem that no single module can solve,
  because memory retrieval, skill loading, protocol schemas, tool descriptions and the model's own
  reasoning traces all compete for the same finite allocation, and the optimal split depends on the
  current phase of execution.
- It reads the convergence of structurally similar harnesses across products with different lineages
  as analytically significant — evidence that the six dimensions are structural requirements of
  externalized agency rather than incidental implementation choices.

## Notes

The authors draw on the tradition of distributed and extended cognition for its engineering insight —
that the boundary between agent and environment is a design choice with real performance
consequences — while stating explicitly that they do not commit to that tradition's stronger
ontological claims. They describe their focus as pragmatic, measuring the value of externalization by
the reliability, composability and governability of the resulting system.

The review positions itself against existing surveys of retrieval-augmented generation, tool
learning, agent architectures and protocol interoperability, arguing that what remains underdeveloped
is not another component-level survey but a common account of *why* these developments are converging
as forms of externalization.

It also emphasises that the dimensions do not evolve independently: memory expansion competes with
skill loading for context budget, protocol standardisation improves interoperability while
constraining how capabilities are packaged, and skill execution generates traces that later become
memory.

See [[DefinedTerm/externalization]] for the organising concept and
[[DefinedTerm/harness-engineering]] for the unifying layer.
