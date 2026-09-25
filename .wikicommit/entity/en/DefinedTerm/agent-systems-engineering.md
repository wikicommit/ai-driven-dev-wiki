---
title: "Agent Systems Engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agents, agent-architecture, reliability, observability]
aliases: ["智能体系统工程化"]
sources:
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/agent/engineering/'
    hash: sha256:ba3ef8f424b5b76f1af59a9b3a243e05ffacad7327edcda8e2f9e42bc81e3099
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "The move, as framed in a chapter of Jimmy Song's online handbook 智能体构建指南, from agents that merely run to agent systems that are reproducible, extensible, observable and maintainable, by adding replay, version tracking, monitoring and error recovery around the model rather than tuning prompts."
---

Agent systems engineering (智能体系统工程化) is the name a draft chapter of Jimmy Song's online handbook
智能体构建指南 gives to taking an LLM-based agent from something that runs to something that can be
reproduced, extended, observed and maintained. The chapter argues that "writing a few prompts and
wiring a few tools" only creates an illusion of simplicity: from a systems-engineering viewpoint the
complexity has not gone away but moved, and frameworks such as LangChain, Flowise and Bailian (百炼)
make an agent run without making it reproducible. Its thesis is that the uncertainty of intelligence
has to be supported by engineering certainty, and it closes on the claim that an agent's
competitiveness lies not in being smarter but in being more reliable.

## Usage

The chapter organises the idea around several tables of its own:

- **Three layers of complexity** — runnability (the demo works; framework encapsulation hides the
  complexity), reproducibility (behaviour can be explained and replayed; what is missing is tracing and
  state management) and evolvability (learning, feedback and iteration; what is missing is system
  design and accumulated knowledge). Complexity, it says, is not eliminated but shifts from the
  development stage to the runtime stage.
- **Uncertainty amplification** — because each LLM call is probabilistic, errors compound across calls:
  if one call is right 90% of the time, a system of 10 calls is right about 35% of the time and one of
  20 calls about 12% (see [[DefinedTerm/compositional-reliability]]). The chapter traces the
  amplification to memory (uncontrolled state consistency, semantic drift in embedding retrieval),
  orchestration (the LLM deciding the flow dynamically) and testing (probabilistic output defeating
  conventional unit tests).
- **From Prompt Hack to system design** — adjusting prompts until a demo works gives no
  reproducibility, extensibility or controllability; the chapter's counterparts are versioning plus
  replay, modular memory plus orchestration, and observability and logging.
- **Stability before intelligence, observability before optimisation** — the core mechanisms it names
  are replay of task execution, version tracking of prompts, memory and RAG, monitoring metrics such as
  success rate, drift rate and redundant-call rate, and error recovery through checkpoints and fault
  tolerance to prevent dead loops and crashes.
- **Five stages of growth** — Hello World (a runnable demo; prompt experiments), scenario stitching
  (tools plus RAG; context management), systematisation (multi-agent collaboration; state consistency),
  engineering deployment (production use; observability and security) and intelligent evolution
  (autonomous learning; long-term memory and feedback loops).
- **A roadmap by layer** — a run layer supported by frameworks, an observation layer (logs, replay,
  version control, metrics), a control layer (recovery, verification, security boundaries) and an
  evolution layer (self-learning and feedback-driven optimisation).

It also lists engineering design patterns — [[DefinedTerm/react-prompting]], [[DefinedTerm/codeact]],
tool use through [[DefinedTerm/model-context-protocol]], self-reflection with a critic model,
multi-agent workflows and agentic RAG — and characterises the framework landscape by saying that
[[SoftwareApplication/langchain]] lets an agent be assembled but loses the ability to explain it,
while [[SoftwareApplication/langgraph]] and LangSmith aim to restore system-level controllability and
observability. Its stated future directions treat an agent as a microservice, orchestration as
distributed-system scheduling, memory as a knowledge graph plus a state database, and observability
as AI-native telemetry.

## When It Applies

The chapter frames this as what an agent needs in order to move from the laboratory into production;
it is aimed at agents built on LLMs whose behaviour varies from run to run. Its counter-example is the
Prompt Hack: tuning prompts is acceptable at the experimental stage, but the chapter holds that it
cannot guarantee stability or maintainability in production, where changing a prompt gives no
assurance of stable behaviour and multi-task prompts proliferate.

It is one author's framing, in a chapter the handbook marks as a draft. The 90% per-call figure is
offered as an assumption to illustrate the compounding, not as a measurement, and the chapter reports
no evaluation of the practices it recommends.

## Related Terms

- [[DefinedTerm/compositional-reliability]] — the compounding of per-step error that the chapter's
  amplification argument rests on
- [[DefinedTerm/llm-based-multi-agent-system]] — the systematisation stage's multi-agent collaboration
- [[DefinedTerm/react-prompting]], [[DefinedTerm/codeact]] — patterns the chapter lists
