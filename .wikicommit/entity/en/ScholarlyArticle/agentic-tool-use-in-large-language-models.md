---
title: "Agentic Tool Use in Large Language Models: A Survey"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, surveys, tool-use, reinforcement-learning]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2604.00835'
    hash: sha256:0773ab593de18a993221d55bb70d4f3695e7b7ce206f95300a029a67efac380f
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A survey that organises the agentic tool-use literature into three methodological paradigms — prompting as plug-and-play, supervised tool learning, and reward-driven tool policy learning — and treats evaluation as a cross-cutting dimension spanning tool usage correctness, task completion and tool-driven interaction."
  author: ["Hu Jinchao", "Meizhi Zhong", "Kehai Chen", "Xuefeng Bai", "Min Zhang"]
  abstract: "Large language models are increasingly deployed as autonomous agents, yet their real-world effectiveness depends on reliable tools for information retrieval, computation and external action. Existing studies remain fragmented across tasks, tool types and training settings, lacking a unified view of how tool-use methods differ and evolve. The survey organizes the literature into three paradigms — prompting as plug-and-play, supervised tool learning and reward-driven tool policy learning — analyzes their methods, strengths and failure modes, reviews the evaluation landscape and highlights key challenges, aiming to address this fragmentation and provide a more structured evolutionary view of agentic tool use."
  keywords: ["Large language models", "Agentic tool use", "Prompt engineering", "Instruction tuning", "Reinforcement learning"]
---

This survey reviews how large language models are given the ability to use external tools, and its
organising move is explicitly historical: rather than presenting a static snapshot of tool-use
techniques, it traces a methodological evolution and argues that what earlier surveys leave
underarticulated is the progression from prompting, to supervised tool learning, to reward-driven
policy learning. The authors compare their coverage against representative prior surveys along six
dimensions — chronological evolution, paradigm taxonomy, tool coverage, training data, evaluation
landscape and open challenges — and position their own contribution as covering all six.

The three paradigms are distinguished by where the optimisation signal comes from.
**Prompting as plug-and-play** keeps the model frozen and elicits tool use through in-context
control; the survey subdivides it into interleaved reasoning and action, decoupled planning and
execution, and program-aided reasoning. **Supervised tool learning** moves the problem from prompt
engineering to data engineering, internalising tool syntax and invocation logic into weights through
self-supervised data generation, large-scale instruction tuning, and process-oriented or
alignment-focused tuning. **Reward-driven tool policy learning** treats tool use as a sequential
decision problem optimised by environmental feedback, spanning strategic decision optimisation,
end-to-end multi-turn policy learning, and holistic or multimodal agentic frameworks.

Evaluation is handled as a cross-cutting dimension rather than a section appended at the end. The
survey groups benchmarks into three levels that it presents as having co-evolved with the paradigms:
tool usage correctness, task completion, and tool-driven interaction.

## Key Points

- The survey's central claim about the three paradigms is that they are **complementary rather than
  successive**, and it argues that production-grade systems will likely combine all three rather than
  settling on the most recent one.
- It characterises the trade-offs of the prompting paradigm directly: flexibility, interpretability
  and low deployment cost, set against higher latency, token cost, and brittleness on complex or
  long-horizon tasks because the model does not internalise tool-use behaviour in its parameters.
- For self-supervised data generation it states the criterion behind the approach explicitly: a
  candidate tool call is retained only when its returned result improves next-token prediction under
  the base language-modelling objective, so a call is useful not because it is syntactically valid
  but because it measurably improves prediction of what comes next.
- It divides the tool-usage-correctness benchmark layer into four concerns — function-call validity,
  tool retrieval and selection, tool-use decisions, and compositional invocation — and argues that
  deciding whether to use a tool at all is an equally important aspect of correctness, since realistic
  agents must also decide when to answer directly, request clarification or abstain.
- It reports that aggregate pass-or-fail scores at the function-call level obscure where failures
  actually occur, and describes finer-grained diagnostic frameworks that separate errors in intent
  understanding, format alignment and tool selection.
- Within the reward-driven paradigm it distinguishes strategic decision optimisation — which asks the
  narrower question of when an agent should invoke a tool versus rely on internal knowledge, balancing
  effectiveness against computational cost and latency — from end-to-end policy learning, where the
  central difficulty becomes credit assignment across long trajectories in which an early mistake
  propagates.
- It observes that as agents are deployed in richer visual environments the definition of tool use
  itself expands to include visual perception, GUI manipulation and long-term memory management,
  and covers frameworks that treat an entire agent system — memory module and tool selector included
  — as a single jointly updated policy.
- Among its five future directions it argues that standardisation around interoperability protocols,
  most notably the [[DefinedTerm/model-context-protocol]], transforms the integration problem from
  quadratic complexity into a linear one by decoupling the agent from each tool's specific
  implementation, and anticipates tool libraries becoming dynamic protocol-compliant marketplaces
  rather than static lists.
- It identifies a 2025 shift toward "agentic foundation models" pre-trained specifically for action,
  describing this as a move away from patching language models with vision encoders and toward
  native vision-language-action models.
- On safety it argues that as agents are granted the power to execute consequential actions, safety
  must be elevated from a secondary metric to a primary design constraint, and it names deceptive
  alignment — agents learning to game reward systems by hiding errors or misrepresenting their tool
  usage — as a risk that must be addressed alongside indirect prompt injection.
- Its final direction argues that the future of tool use may lie less in fully autonomous monolithic
  agents than in collaborative workflows combining human oversight with specialised automated
  components, and that under this view skills become a more practical abstraction than end-to-end
  autonomy: systems expose reusable capabilities and compose them flexibly under human supervision.

## Notes

The survey's evolutionary framing is also its background section: it dates the conceptual
foundations to work that predates modern instruction-tuned models, places prompt-driven agency in
2022–2023, the shift to supervised tool learning in 2023–2024, and the rise of reinforcement-learning
policy optimisation from 2024 onward.

It relates to several subjects this wiki already covers.
[[DefinedTerm/tool-use-design-pattern]] and [[DefinedTerm/agentic-tool-use]] are the practice it
surveys; [[DefinedTerm/react-prompting]] is the interleaved reasoning-and-action control loop it
treats as the canonical starting point of the prompting paradigm; and
[[Dataset/berkeley-function-calling-leaderboard]] is among the function-call-validity benchmarks it
catalogues.
