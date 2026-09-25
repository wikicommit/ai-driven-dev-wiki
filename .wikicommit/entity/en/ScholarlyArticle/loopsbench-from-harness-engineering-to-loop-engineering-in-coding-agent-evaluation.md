---
title: "LoopsBench: From Harness Engineering to Loop Engineering in Coding Agent Evaluation"
type: "schema:ScholarlyArticle"
lang: en
tags: [benchmarks, evaluation, coding-agents, loop-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2608.00267'
    hash: sha256:da50e26db4b6652f26795f68836e4fb8270bec5379729dc7b256336acbb4f230
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A preprint introducing LoopsBench, a long-horizon benchmark that represents each coding task as a dependency DAG of separately testable development units, releases tests along the ready frontier and keeps completed units as regression obligations, and uses recorded loop traces to evaluate models and loop implementations together."
  author: ["Han Li", "Zhemin Fang", "Rili Feng", "Yingqi Zhao", "Jiaheng Liu", "Pengfei Gao", "He Ye", "Dayi Lin", "Qingwei Lin", "Saravan Rajmohan", "Dongmei Zhang"]
  abstract: "Coding agent infrastructure is shifting from harness engineering toward loop engineering as coding agents are deployed for sustained long-horizon software development, while existing benchmarks center on localized tasks or end-state outcomes. LoopsBench is a long-horizon benchmark for loop engineering in coding agent evaluation in which each task is a dependency DAG over separately testable development units with source-evidenced prerequisite edges. It comprises 112 tasks from authentic sources spanning 8 programming languages and 9 domains, and its flow-aware runtime releases tests along the ready frontier and retains completed nodes as regression obligations. The strongest configuration, Opus-4.7 with Claude Code and outer continuation, resolves 25.00% of tasks; recorded plans recover only part of the source-recovered prerequisite DAG, and regression events remain visible across the evaluated loop profiles."
  keywords: ["loop engineering", "coding agents", "long-horizon benchmark", "dependency DAG", "regression obligations"]
---

This preprint, with authors from Microsoft, Nanjing University, University College London and
Shanghai Jiao Tong University, argues that coding agent systems increasingly expose loop mechanisms
for sustained software work — it names Codex goal mode, Claude Code goal mode and Claude Code dynamic
workflows — that add a higher-level control surface over the harness rather than replacing it. The
core challenge, in the authors' framing, therefore moves from [[DefinedTerm/harness-engineering]]
alone to [[DefinedTerm/loop-engineering]] over the harness, where the loop must govern execution
across task structure, state continuity and regression pressure as dependent work accumulates.

Existing benchmarks such as [[Dataset/swe-bench]] and its variants, the authors argue, remain
largely terminal: agents receive self-contained issues or flat specifications and are judged by final
task success, which does not reveal whether an agent preserves intermediate obligations, avoids
regressions, or follows a viable order through dependent subproblems. Their answer is
[[Dataset/loopsbench]], in which each task is a dependency DAG of source-grounded development units,
and an evaluation runtime releases each unit's tests only once its prerequisites pass, keeps completed
units' tests active as regression obligations, and records a loop trace while leaving the execution
order to the evaluated loop. The authors describe it as, to their knowledge, the first benchmark for
loop engineering evaluation.

The experiments are organized around three questions — how far current loops sustain progress, how
they maintain plan, code and test state, and which loop engineering factors shape long-horizon
execution — and evaluate frontier models paired with widely used loop implementations, including
[[SoftwareApplication/claude-code]], [[SoftwareApplication/openai-codex]],
[[SoftwareApplication/github-copilot]], [[SoftwareApplication/openhands]] and
[[SoftwareApplication/swe-agent]].

## Key Points

- The strongest configuration, Opus-4.7 under Claude Code with outer continuation, resolves 25.00% of
  the 112 tasks, and every model and loop configuration evaluated remains well below full resolution.
- Model scaling within a family under its vendor's loop, model sweeps under a fixed loop, and loop
  sweeps under a fixed model all fall short, which the authors take to mean long-horizon limitations
  are not explained by model choice or loop implementation in isolation.
- Without the benchmark's outer continuation loop, a single execution segment usually reaches only a
  shallow prefix of the dependency structure; external continuation reduces early stalls and increases
  partial progress.
- Recorded plans recover only part of the source-recovered prerequisite DAG. Closed-source loop
  implementations organize execution as a tree-shaped concurrent structure close to the reference
  DAG's concurrency, while open-source implementations driven by linear control flow form a near
  chain.
- On units the evaluated loops resolve, their patches are longer than the gold reference by a
  consistent margin, and the loops author far fewer tests than the native suites, leaving earlier
  obligations with limited regression protection; deployed loop implementations regress on several
  percent of previously satisfied obligations.
- Among four loop runs compared on context renewal, Claude dynamic workflows (task-specific workers
  with narrower contexts) reach the highest resolve rate at 24.11% and the Ralph loop the lowest at
  7.84%, but regression events appear in all four profiles, so renewing context does not remove
  regression pressure.
- The authors conclude that long-horizon coding agents should be evaluated with joint attribution to
  model choice and loop configuration, especially residual work handling, structured state and
  regression obligation retention.

## Notes

The authors state that the recovered DAG is a lower bound on prerequisite structure rather than a
complete causal graph, that the fixed DAG is an evaluation contract under which unit boundaries and
reference patches are not unique, and that the task pool excludes mobile, frontend-heavy and
hardware-adjacent projects. They caution that the correctness metrics measure executable obligations
rather than full semantic equivalence, that model-assisted materialization may bias wording and tests,
and that public sources leave contamination risk. They note that the four context-renewal runs used
their native model and loop configurations and so characterize observed loop profiles rather than a
controlled causal comparison. The runs compared include the [[DefinedTerm/ralph-loop]].
