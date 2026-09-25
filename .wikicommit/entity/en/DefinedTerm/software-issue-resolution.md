---
title: "Software Issue Resolution"
type: "schema:DefinedTerm"
lang: en
tags: [agents, software-maintenance]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2512.22256'
    hash: sha256:9a5a75e55b1a5f5818704198234c0c775aeeaaf8ae884348416af572766c9cd2
  - type: url
    url: 'https://arxiv.org/pdf/2601.11655'
    hash: sha256:cbedafca04b35cddb49e45fd2b158a2fc521a51a9ea5da37f4059553ec41b806
  - type: url
    url: 'https://arxiv.org/html/2406.01422v2'
    hash: sha256:d9bfa615cea940d9674ffc433e47eb528cb25093699809cd3e9b54dabf0caf1d
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "The task of understanding, locating and resolving issues in a real code repository from a developer's natural-language description of the problem, producing a repository-level patch. It spans diverse maintenance activities — bug fixes, feature additions, efficiency optimisation — and does not assume a test exists that triggers the reported behaviour."
---

**Software issue resolution** is the task of understanding, locating and resolving issues in
real-world code repositories on the basis of developers' natural-language descriptions of them. In
its automated, end-to-end form it takes an issue description and a code repository as input and
produces a repository-level patch that resolves the issue. It covers diverse maintenance activities,
including bug fixes, feature additions and efficiency optimisations, and it is a part of software
maintenance, which
[[ScholarlyArticle/agentic-software-issue-resolution-with-large-language-models]] reports as
accounting for about two-thirds of software lifecycle costs.

## Usage

The term is used to mark out a task boundary. That survey argues that issue resolution should not be
treated as a sub-case of automated program repair, on two grounds: it encompasses more diverse
maintenance activities than repair does, and — even for bug-fixing issues — it does not assume the
existence of tests that can trigger the bug. The second point has consequences for how a system is
built, since generating a test that reproduces the reported behaviour becomes part of the work rather
than a given.

The same survey abstracts the automated task into five logical phases, which it stresses denote
functions rather than a fixed execution order, so a system may run them sequentially or interleave
them dynamically at inference time:

- **Repo preprocessing** — constructing an accessible, comprehensible knowledge representation of the
  repository, such as a tree of files, classes and functions or a graph that additionally encodes
  calls, inheritance, imports and references.
- **Localization** — identifying the code snippets most likely responsible for the reported issue,
  narrowing the search space for the phases that follow.
- **Repair** — generating candidate patches for the located code, typically several, to maximise the
  chance of producing a correct fix.
- **Patch validation** — generating reproduction tests that simulate the issue scenario, or selecting
  regression tests that check the candidate patch has not broken existing behaviour, and filtering
  out patches that fail.
- **Patch selection** — choosing the most promising candidate for submission, by self-consistency
  voting over normalised patches or by having a model assess each candidate against the issue.

The survey is explicit that the phases are diagnostic rather than sufficient: dedicated localization
methods have been shown to raise end-to-end resolution rates when fed into downstream patch
generation, and generated reproduction tests are widely used to filter and rerank candidates, but
correct localization does not guarantee a correct patch and weak reproduction tests may accept
patches that are plausible yet behaviourally incorrect.

[[ScholarlyArticle/advances-and-frontiers-of-llm-based-issue-resolution]] gives the task a formal
statement rather than a phase decomposition, and the two are compatible. An instance is written as
`I = (D, C, T)` — an issue description, a codebase and corresponding tests — of which only `D` and
`C` are observable during resolution, alongside an environment `E` that can be explored; a method is
expected to produce a patch `P = M(D, C, E)`, which is applied and then evaluated by running `T`.
The aggregate metric that survey uses is the **Resolved Rate**, the mean of per-instance binary
outcomes over a dataset.

That survey organises the methods literature into training-free and training-based halves.
Training-free methods are grouped by framework (single-agent, multi-agent and fixed-workflow
designs), by plug-and-play module (tools for repository interaction, memory for experience
accumulation) and by inference-time scaling, which uses search or parallelisation to raise success
rates without changing model parameters; training-based methods split into supervised fine-tuning
and reinforcement learning. Its own statistics report [[SoftwareApplication/openhands]] as the most
prevalent scaffold for reinforcement-learning rollouts, followed by workflow-based methods — notably
[[DefinedTerm/agentless]] and two-stage workflows — with environment-native frameworks such as
R2E-Gym and SWE-Gym also frequently adopted because they align with training data.

The same survey is pointed about the task's evidence base. It reports that agent success rates are
frequently inflated by solution leakage, ambiguous issue descriptions and weak test suites that fail
to catch incorrect patches, and that because manual cleanup is too costly and inconsistent at scale
the field is shifting toward automated validation using model-based consensus to separate valid fixes
from false positives. Among the open problems it names are the absence of efficiency-aware
evaluation — resolve rates are measured while API cost and inference time are not, obscuring the
computational and economic burden of high-performing methods — and the reliance on outcome-level
rewards, typically a binary test pass or fail, which it argues makes credit assignment ambiguous
across the many action steps a multi-turn task requires.

One system shows what the repo-preprocessing and localization phases look like when a method invests
heavily in them. [[ScholarlyArticle/lingmaagent-improving-automated-issue-resolution]] argues that a
comprehensive understanding of the whole repository is the most critical path to automating the task,
because the code making up one functionality is typically scattered across folders and files and
cannot all be placed in a model's context. Its agent builds a knowledge graph of files, classes,
functions and function calls, explores it with Monte Carlo tree search before attempting a fix, and
reports higher fault-localization accuracy than the agent baselines it compares against. The same
paper gives an industrial data point on how far automation reaches: on issues drawn from Alibaba
Cloud's own repositories its agent resolved 16.9% unaided, and on a 30-issue subset the rate rose to
43.3% once engineers could adjust its plans, searches and fault localization — which the authors read
as the system augmenting human problem-solving rather than replacing it.

## Related Terms

- [[DefinedTerm/ai-coding-agent]] — the kind of system the task is now predominantly attempted with
- [[DefinedTerm/repository-level-coding]] — the broader setting the task operates in
- [[Dataset/swe-bench]] — the benchmark whose introducing paper the survey credits with pioneering the task
- [[ScholarlyArticle/advances-and-frontiers-of-llm-based-issue-resolution]] — a survey of the task's data, methods and analysis literature
- [[ScholarlyArticle/lingmaagent-improving-automated-issue-resolution]] — an agent built around whole-repository exploration
