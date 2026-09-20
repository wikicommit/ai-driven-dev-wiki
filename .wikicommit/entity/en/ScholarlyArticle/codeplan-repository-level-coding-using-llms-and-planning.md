---
title: "CodePlan: Repository-level Coding using LLMs and Planning"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, llm, software-engineering, legacy-modernization]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2309.12499'
    hash: sha256:19aa6b297c4058cd751158ab0079977a52e09e89b57a947614dda5da3fa328da
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The arXiv preprint that frames repository-level coding as a planning problem and presents CodePlan, a task-agnostic framework that synthesizes a multi-step chain of edits across an entire code repository."
  author: ["Ramakrishna Bairi", "Atharv Sonwane", "Aditya Kanade", "Vageesh D C", "Arun Iyer", "Suresh Parthasarathy", "Sriram Rajamani", "B. Ashok", "Shashank Shet"]
  datePublished: "2023-09-21"
  abstract: "The paper formulates software engineering activities that pervasively edit an entire repository — package migration, fixing error reports from static analysis or testing, adding type annotations or other specifications — as repository-level coding tasks, and argues they cannot be solved directly by LLMs because code within a repository is inter-dependent and the repository may be too large to fit into a prompt. It frames the problem as planning and presents CodePlan, a task-agnostic framework that synthesizes a multi-step chain of edits in which each step calls an LLM on a code location with context derived from the whole repository, previous changes and task-specific instructions, built on a combination of incremental dependency analysis, change may-impact analysis and an adaptive planning algorithm. Evaluated on package migration in C# and temporal code edits in Python, CodePlan is reported to match ground truth better than baselines and to get 5 of 6 repositories through validity checks where the baselines get none."
---

This arXiv preprint takes a class of software engineering work that touches a whole codebase at
once — package migration, fixing error reports from static analysis or testing, and adding type
annotations or other specifications — and formulates it as
[[DefinedTerm/repository-level-coding]]. The authors' argument for treating these separately is that
tools such as GitHub Copilot, powered by large language models, have succeeded at localized coding
problems, while repository-level tasks cannot be solved directly using LLMs: code within a
repository is inter-dependent, and the entire repository may be too large to fit into the prompt.

The paper's response is to frame repository-level coding as a planning problem and to present
CodePlan, a task-agnostic framework for solving it. CodePlan synthesizes a multi-step chain of
edits — a plan — in which each step results in a call to an LLM on a particular code location, with
context derived from the entire repository, from previous code changes, and from task-specific
instructions. The authors describe the framework as resting on a novel combination of three
ingredients: an incremental dependency analysis, a change may-impact analysis, and an adaptive
planning algorithm.

CodePlan is evaluated on two repository-level tasks — package migration in C# and temporal code
edits in Python — each across multiple repositories requiring inter-dependent changes to between 2
and 97 files. The authors state that coding tasks of this level of complexity have not been
automated using LLMs before. They report that CodePlan matches the ground truth better than the
baselines, and that CodePlan gets 5 of 6 repositories to pass the validity checks — for example
building without errors and making correct code edits — while the baselines, which have the same
type of contextual information but no planning, get none of the repositories to pass.

The paper is filed under Software Engineering (cs.SE), was submitted on 21 September 2023 as version
1, and carries the arXiv-issued DOI 10.48550/arXiv.2309.12499.

## Key Points

- The paper formulates package migration, fixing error reports from static analysis or testing, and adding type annotations or other specifications as repository-level coding tasks — activities that involve pervasively editing an entire repository.
- Its stated reason these resist direct LLM use is twofold: code within a repository is inter-dependent, and the entire repository may be too large to fit into the prompt.
- CodePlan is presented as a task-agnostic framework that treats the problem as planning, synthesizing a multi-step chain of edits where each step calls an LLM on one code location with context drawn from the whole repository, prior changes, and task-specific instructions.
- The framework is described as a novel combination of incremental dependency analysis, change may-impact analysis, and an adaptive planning algorithm.
- The reported evaluation covers two tasks and six repositories in total: CodePlan gets 5 of 6 repositories through the validity checks while the planning-free baselines get 0 of 6 — a comparison in which the baselines are given the same type of contextual information, so the difference the authors attribute it to is the planning.

## Notes

The baselines are constructed to isolate one variable: the abstract states they carry the same type
of contextual information as CodePlan and differ in not planning. The evaluation's scale is small in
repository count — six in total across the two tasks — while the per-repository change is large, at
between 2 and 97 files. The authors' claim that tasks of this complexity have not been automated
using LLMs before is stated in the abstract as their own assessment of the prior state of the art.
