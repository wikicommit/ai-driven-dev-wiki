---
title: "Four-Stage Evolution of Agentic Engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agents, agentic-engineering, autonomy-levels]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.05608'
    hash: sha256:0793091fcad2dc48f9eb6412001558cc2e993e5d5904e18d8fd0c943453879be
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A proposed four-stage roadmap for agentic engineering — tool-augmented assistance, single-task autonomy, coordinated multi-agent teams, and self-evolving ecosystems — each stage characterised by an agent capability, the enabling technologies, and the human role that remains."
---

The four-stage evolution of agentic engineering is a roadmap proposed in
[[ScholarlyArticle/agentic-software-restructuring-paradigm]], based on what the paper describes as
current capabilities and trajectories. Each stage is characterised along four axes: what the agent can
do, the key technologies that enable it, what the human role becomes, and which systems are
representative of it.

## Usage

**Stage I, Tool-Augmented (2023–2025)**, is the mode the paper identifies as currently dominant. Agents
serve as assistants within human-led workflows, handling code completion, single-issue fixes and simple
script generation through in-context learning and retrieval. The human is author and reviewer.
[[SoftwareApplication/github-copilot]] and [[SoftwareApplication/claude-code]] are named as
representative. The limitation is that the human must still decompose problems, design architecture and
verify correctness.

**Stage II, Single-Task Autonomous (2025–2027)**, has agents own complete tasks from specification to
deployment — end-to-end feature building, debugging, basic system maintenance — through planning, tool
use and self-correction. The human shifts to intent architect and auditor: from doing, to specifying
what to do and verifying what was done. [[SoftwareApplication/devin]] and OpenHands are named as
demonstrating that agents can autonomously navigate codebases, implement features and submit pull
requests.

**Stage III, Multi-Agent Teams (2026–2029)**, has specialised agents coordinate as teams mirroring human
engineering organisations: a product-manager agent translating business requirements into technical
specifications, architect agents designing structure, developer agents implementing components, QA
agents testing and validating. The enabling technologies are shared memory, role specialisation and
orchestration; shared memory and observability become critical infrastructure. The human role becomes
PM plus architect plus auditor, and LangChain orchestration and MetaGPT are named as representative.

**Stage IV, Self-Evolving Ecosystems (2028+)**, has agents improve their own architectures, spawn
specialised sub-agents for new problem domains, and adapt to environmental change without human
intervention. At this stage, the paper argues, the distinction between software and agent dissolves
entirely — the agent is the system and evolves continuously — and human involvement shifts to
meta-level governance: setting ethical boundaries, defining value functions and ensuring alignment. Its
representative systems are given as prospective rather than existing.

## When It Applies

The scheme is a forecast, and its stage boundaries are the paper's own reading of a trajectory rather
than thresholds with a stated measurement behind them. The date ranges given for the stages overlap, which fits a
roadmap describing what becomes possible rather than what replaces what; the paper does not comment on
the overlap.

It assumes the capability trend it extrapolates from continues. The paper's own empirical section is
the place to read against that assumption: it reports the [[Dataset/evoclaw]] benchmark's finding that
success rates collapse from above 80% on isolated tasks to at most 38% on continuous software
evolution, and treats the gap between those two numbers as quantifying the distance still to be
covered. On the paper's own account that gap is not fundamental — it reflects limitations in context
management, memory architecture and verification that are active research areas — but the paper states
directly that fully autonomous software development will require several more years of concentrated
research before it is reliable in production.

Used as a positioning device the scheme is one of several. It is a distinct scheme from
[[DefinedTerm/agentic-autonomy-levels]] and [[DefinedTerm/se-autonomy-levels]], which cut the same
territory differently; nothing in this source reconciles it with either, and a reader comparing them
should treat the stage numbers as internal to this paper.

## Related Terms

- [[ScholarlyArticle/agentic-software-restructuring-paradigm]] — the paper that proposes this roadmap
- [[DefinedTerm/agentic-engineering]] — the discipline whose evolution the stages describe
- [[DefinedTerm/agentic-autonomy-levels]] — a separate scheme over similar ground
- [[DefinedTerm/se-autonomy-levels]] — another such scheme
- [[Dataset/evoclaw]] — the benchmark whose results the same paper uses to locate current capability
