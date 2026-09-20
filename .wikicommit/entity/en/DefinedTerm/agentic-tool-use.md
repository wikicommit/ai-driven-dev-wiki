---
title: "Agentic Tool Use"
type: "schema:DefinedTerm"
lang: en
tags: [agents, tool-use, agent-architecture]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.00835'
    hash: sha256:0773ab593de18a993221d55bb70d4f3695e7b7ce206f95300a029a67efac380f
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The mechanism by which a language model acting as an agent invokes external tools — APIs, databases, code interpreters — to access current knowledge, perform precise computation and act on external systems, rather than answering from its parameters alone."
---

**Agentic tool use** is the mechanism that operationalises action in an agentic system: a language
model serving as the reasoning core invokes external tools — APIs, databases, code interpreters and
the like — so that it can access up-to-date knowledge through search, improve computational accuracy
through programmatic execution, and perform real-world operations through external systems.
[[ScholarlyArticle/agentic-tool-use-in-large-language-models]] motivates it by what a standard model
cannot do on its own: its knowledge is bounded by its training data, which can produce factual errors
or hallucinations, and it struggles to access real-time information, execute precise computation, or
interact reliably with external systems.

## Usage

That survey organises the practice into three paradigms distinguished by where the optimisation
signal comes from, and presents them side by side as complementary rather than as successive
replacements.

- **Prompting as plug-and-play.** The model's parameters stay frozen and tool-use behaviour is
  elicited through instructions, demonstrations and feedback from the environment. The survey
  subdivides it into interleaved reasoning and action (a loop that alternates deliberation with
  external operations, using each observation to guide the next decision), decoupled planning and
  execution (a structured plan is produced first and then carried out, reducing repeated deliberation
  at every step), and program-aided reasoning (the intermediate representation shifts from text to
  executable code, making the program executor part of the reasoning process rather than an auxiliary
  utility).
- **Supervised tool learning.** Tool-use patterns are encoded directly into model parameters using
  labelled or synthetic supervision, which the survey frames as a shift from prompt engineering to
  data engineering. Its three strands are self-supervised data generation, large-scale instruction
  tuning across broad API corpora, and process-oriented or alignment-focused tuning that optimises
  the reasoning leading to a tool call rather than only the call's correctness.
- **Reward-driven tool policy learning.** Tool use is treated as a sequential decision problem
  optimised through environmental feedback rather than imitation. Its strands are strategic decision
  optimisation (when to invoke a tool versus rely on internal knowledge), end-to-end policy learning
  over multi-turn interaction, and holistic or multimodal frameworks that optimise an entire agent
  system — memory module and tool selector included — as one policy.

The same survey treats evaluation as a cross-cutting dimension with three levels that it says have
co-evolved with the paradigms: **tool usage correctness** (can the model produce structurally valid
calls, retrieve and select the right tool, and decide whether a tool is needed at all),
**task completion** (can it finish an end-to-end task with tools as functional components of the
solution), and **tool-driven interaction** (can it act reliably in dynamic, stateful environments
where its actions change the external world, including under adversarial conditions).

## When It Applies

- Applies where a task needs information, computation or effects that the model's parameters cannot
  supply — current knowledge, exact arithmetic, or changes to an external system. The survey's
  framing is that these are recurrent mismatches between what models are good at and what deployment
  requires, not incidental gaps.
- Assumes a tool surface the model can be made to address correctly. The survey's evaluation section
  treats schema compliance, retrieval from a large candidate pool, and correct argument grounding as
  separate abilities that can each fail independently, which is why it separates diagnostic
  benchmarks from end-to-end ones.
- Fails in ways that differ by paradigm, which is the survey's argument for keeping all three in
  view. Prompting is flexible and cheap to deploy but suffers higher latency and token cost and
  becomes brittle over long horizons. Supervised learning is more efficient and stable but depends on
  obtaining large-scale, high-quality trajectory data. Reward-driven learning addresses exploration
  and error recovery but faces credit assignment across long trajectories where an early mistake
  propagates.
- Fails, too, when it is applied where it is not needed. The survey notes that many earlier
  benchmarks implicitly assume a tool should be called, and reports work showing that unnecessary
  invocation can degrade overall performance even when the tool is available — which is why
  deciding *not* to use a tool is treated as part of correctness.
- Well established as a research area with a substantial benchmark ecosystem, but the survey is
  explicit that its own unifying claim — that production-grade systems will combine all three
  paradigms — is its authors' synthesis rather than a measured result.

## Related Terms

- [[DefinedTerm/tool-use-design-pattern]]
- [[DefinedTerm/react-prompting]]
- [[DefinedTerm/plan-then-execute-pattern]]
- [[DefinedTerm/code-then-execute-pattern]]
- [[DefinedTerm/model-context-protocol]]
- [[DefinedTerm/ai-agent]]
