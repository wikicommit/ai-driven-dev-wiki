---
title: "Agentic Software: How AI Agents Are Restructuring the Software Paradigm"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, agentic-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.05608'
    hash: sha256:0793091fcad2dc48f9eb6412001558cc2e993e5d5904e18d8fd0c943453879be
review_status: pending
generated_at: "2026-09-18"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An argument that AI agents restructure what software is rather than improving how it is built, formalizing the distinction between deterministic and agentic software and proposing a four-stage roadmap toward self-evolving agent ecosystems."
  author: ["Zhenfeng Cao"]
  datePublished: "2026-06-11"
  keywords: ["agentic software", "Agent-as-a-Service", "agentic engineering", "software paradigm"]
---

This paper argues that the emergence of AI agents constitutes a restructuring of what software is, not
an incremental tool improvement within the existing paradigm. Its formal move is to define two kinds of
system side by side: a traditional software system as a triple of computational resources,
deterministic decision rules encoded in source code, and an execution environment, where the decision
rules are static with respect to execution and must be written by human engineers before the system
sees any input; and an AI agent system as a tuple of a language model serving as reasoning engine, a
set of executable tools, a memory subsystem, and a planning mechanism, where the decision logic is
generated at runtime. That distinction is the paper's central claim about
[[DefinedTerm/agentic-software]].

The argument for why this matters is a complexity one. The paper invokes Brooks's distinction between
accidental and essential complexity, notes that decades of advances have reduced the former while the
latter remains unbounded, and proposes that the number of possible interaction topologies among a
system's components grows super-exponentially while human cognitive capacity stays essentially
constant. Under the traditional paradigm a task whose solution space exceeds that fixed capacity is
infeasible at any realistic cost; under the agentic paradigm the model traverses the space with a
capacity that scales with model size and training compute, so solution capacity is decoupled from human
cognitive limits.

The paper then traces three generations of software delivery — local licensed software, SaaS, and
[[DefinedTerm/agent-as-a-service]] — as a progressive transfer of complexity away from the end user,
and frames [[DefinedTerm/agentic-engineering]] as an expansion of the software engineering discipline
rather than a replacement for it, distinguished by its core object of study, its control model and the
human role. It closes with a [[DefinedTerm/four-stage-evolution-of-agentic-engineering]] roadmap and
recommendations for practitioners, researchers and organisations.

## Key Points

- The paper makes three central claims: that the agentic paradigm is an inevitable consequence of
  complexity scaling rather than a market preference; that software is redefined rather than replaced,
  since the agent is itself software of a different kind; and that agentic engineering is emerging as a
  distinct practice whose practitioners are not better programmers but a different role — intent
  architects, agent coordinators and outcome auditors.
- The paper argues that in an agentic system the code the model generates is not the system but a
  transient artifact, produced and discarded in service of reasoning goals.
- It positions this as extending rather than restating Karpathy's "Software 2.0" framing: where that
  formulation has neural networks replace hand-crafted program logic with learned weights, the paper
  argues agentic systems go further by writing programs on demand and using code as a tool.
- It identifies three structural weaknesses in the prevailing "AI → Software → Result" pipeline: the
  human engineer remains the critical path for design, architecture, integration and deployment; the
  final deliverable is still a traditional system whose complexity scales with its decision rules; and
  iteration latency cannot fall below human communication and coordination speeds.
- It contrasts traditional software engineering with agentic engineering across nine dimensions
  including core artifact, control centre, decision mechanism, development cycle, human role,
  complexity ceiling, output unit, error handling and evolution.
- The four-stage roadmap runs from Tool-Augmented (2023–2025) through Single-Task Autonomous
  (2025–2027) and Multi-Agent Teams (2026–2029) to Self-Evolving Ecosystems (2028+), with the human
  role shifting from author-and-reviewer to goal setter and ethics governor.
- Among the open problems it names as urgent are long-context state management, verification in
  open-ended settings, agent alignment at scale as agents are composed into teams, and economic models
  for outcome-based pricing.

## Notes

The paper reports no measurements of its own; every data point in its empirical section is a result
cited from other work. Those citations are worth reading as the paper's own framing of external evidence: it reports
[[Dataset/swe-bench-verified]] results for an open development-process-centric model, a pilot study of
coordinated agent swarms across enterprise debugging workflows, and the self-evolution mechanism in
[[SoftwareApplication/hermes-agent]] as evidence for the agentic thesis, while presenting the
[[Dataset/evoclaw]] benchmark as the counterweight.

That counterweight is where the paper sets its own limits. It reports EvoClaw's finding that overall
performance scores drop from above 80% on isolated tasks to at most 38% in continuous settings, reads
four core challenges out of it — context drift, error propagation, absent technical-debt awareness and
verification fidelity — and concludes that the gap between isolated-task performance and sustained
autonomous development quantifies the distance from fully autonomous software engineering. Its own
summary of that position is that agentic engineering is real and transformative today as an
augmentation paradigm, but that several more years of concentrated research are needed before fully
autonomous software development becomes reliable in production.

The paper's account of agentic engineering as a named field attributes the formal introduction of the
term to LangChain in April 2026, and quotes that definition rather than proposing one of its own. Its
stage-based roadmap and its date ranges are presented as a proposal based on current capabilities and
trajectories, with no stated method behind the dates.
