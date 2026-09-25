---
title: "AgileCoder"
type: "schema:SoftwareApplication"
lang: en
tags: [multi-agent, coding-agents, software-process]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2406.11912'
    hash: sha256:0bb6ae4b557525a907cd35ba8c21dc61c06135078855bd330d09e93218f0e09d
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A multi-agent software development framework in which LLM agents playing Agile roles build software from user requirements over successive sprints, supported by a Dynamic Code Graph Generator that keeps a code dependency graph up to date for context retrieval."
  applicationCategory: "Multi-agent software development framework"
  featureList: "Agile roles (Product Manager, Scrum Master, Developer, Senior Developer, Tester); product and sprint backlogs with acceptance criteria; sprints of planning, development, testing and review; three-step static code review; test suites and testing plans derived from a code dependency graph; Dynamic Code Graph Generator; instructor–assistant conversations with a message stream and a global message pool"
---

AgileCoder is a multi-agent software development framework that adapts Agile Methodology to LLM
agents; its repository is given as <https://github.com/FSoft-AI4Code/AgileCoder>. Given user requirements,
agents in Agile roles plan, write, review and test the software incrementally over sprints, with
the framework deciding at the end of each sprint whether to deliver or plan another. It is
introduced in
[[ScholarlyArticle/agilecoder-dynamic-collaborative-agents-for-software-development-based-on-agile-methodology]],
whose authors present it as an alternative to multi-agent systems such as
[[SoftwareApplication/metagpt]] and [[SoftwareApplication/chatdev]], which they describe as following
the waterfall model.

## Capabilities

The Product Manager turns user requirements into a product backlog of development tasks and
acceptance criteria, and the Scrum Master reviews it for feasibility. Each sprint then runs four
phases. In planning, tasks are selected into a sprint backlog. In development, the Developer writes
code annotated with docstrings, and the Senior Developer reviews it statically in three steps:
basic implementation checks such as empty methods and missing imports, compliance with the sprint
backlog, and satisfaction of the acceptance criteria with no bugs. In testing, the Tester writes
test suites for the files changed in the sprint and their ancestor files, and the files are
executed according to a testing plan until bugs or failed tests are reported back to the
Developer. In review, the Product Manager compares an accumulated report with the backlog and
acceptance criteria to decide whether to conclude, in which case the Scrum Master writes
documentation on how to run the software and install its libraries.

The Dynamic Code Graph Generator keeps a Code Dependency Graph whose nodes are code files and whose
edges mainly capture import relations, updating it as the code changes. The graph determines which
files need testing, supplies a logical testing order by reversing a topological order, and, when an
execution error occurs, lets agents trace back from the traceback and retrieve only the relevant
cross-file context instead of the whole codebase. An Execution Environment runs the code and
returns tracebacks to the agents.

Agents talk in two-party conversations between an instructor and an assistant in unconstrained
natural language, continuing until they reach consensus or an exchange limit; a message stream
serves as the conversation's working memory, and a global message pool stores every conversation's
output and the status of each task, from which each conversation reads only the segments relevant
to it.

## Adoption & Ecosystem

The paper runs AgileCoder with GPT-3.5 Turbo, Claude 3 Haiku and GPT-4 as backbone models and
evaluates it on HumanEval, MBPP and [[Dataset/projectdev]], a set of software development tasks the
authors compiled. The authors suggest extending it with further Agile practices such as pair programming,
CI/CD, Kanban or Lean, and applying the approach to domains beyond software development.
