---
title: "AutoCodeRover: Autonomous Program Improvement"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, coding-agents, software-engineering, evaluation]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2404.05427'
    hash: sha256:910627e9213aadf76eec527df275053539dca22c6de64a629ce02ffb7d3e1a5a
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The arXiv preprint that presents AutoCodeRover, an approach combining LLMs with program-structure-aware code search to solve GitHub issues autonomously, reported as resolving 19% of SWE-bench-lite at an average cost of $0.43 per issue."
  author: ["Yuntong Zhang", "Haifeng Ruan", "Zhiyu Fan", "Abhik Roychoudhury"]
  datePublished: "2024-04-08"
  abstract: "The paper argues that software engineering involves program improvement — maintenance such as bug fixing and evolution such as feature additions — apart from coding itself, and proposes AutoCodeRover, an automated approach for solving GitHub issues to achieve program improvement autonomously. AutoCodeRover combines LLMs with code search that works over a program representation, the abstract syntax tree, exploiting classes and methods to sharpen the model's understanding of an issue's root cause, and uses spectrum-based fault localization where a test suite is available. On SWE-bench-lite, 300 real-life GitHub issues, the authors report 19% efficacy at an average cost of $0.43 per issue, higher than the reported efficacy of SWE-agent."
---

This arXiv preprint starts from a distinction between two kinds of work. Researchers have automated
much of the software development process, and recent progress in large language models has let
developers use LLM-based programming assistants to achieve automated coding — but, the authors
argue, software engineering involves the process of *program improvement* apart from coding,
specifically to enable software maintenance, such as bug fixing, and software evolution, such as
feature additions.

The approach the paper proposes for that work is [[SoftwareApplication/autocoderover]], an automated
approach for solving GitHub issues to autonomously achieve program improvement. In it, LLMs are
combined with sophisticated code search capabilities, ultimately leading to a program modification
or patch. The authors contrast their outlook with recent LLM agent approaches from AI researchers
and practitioners, describing theirs as more software engineering oriented: they work on a program
representation — the abstract syntax tree — as opposed to viewing a software project as a mere
collection of files. The code search exploits program structure in the form of classes and methods,
which the authors say enhances the LLM's understanding of the issue's root cause and effectively
retrieves context via iterative search. Where a test suite is available, spectrum-based fault
localization sharpens that context further.

On SWE-bench-lite, described in the paper as 300 real-life GitHub issues, the authors
report increased efficacy in solving GitHub issues at 19%, which they state is higher than the
efficacy of the recently reported SWE-agent. They also report achieving this at significantly lower
cost than other baselines, at an average of $0.43 USD. The paper closes by positing that the
workflow enables autonomous software engineering, in which auto-generated code from LLMs can in
future be autonomously improved.

The paper is filed under Software Engineering (cs.SE) and Artificial Intelligence (cs.AI). It was
first submitted on 8 April 2024 and last revised on 25 July 2024 as version 3, carries the
arXiv-issued DOI 10.48550/arXiv.2404.05427, and was to appear in ISSTA 2024.

## Key Points

- The paper separates program improvement — software maintenance such as bug fixing, and software evolution such as feature additions — from coding itself, and takes the former as its target.
- AutoCodeRover combines LLMs with code search capabilities to produce a program modification or patch in response to a GitHub issue.
- Its stated point of difference from other LLM agent approaches is working on a program representation, the abstract syntax tree, rather than viewing a project as a mere collection of files.
- Code search exploits classes and methods to enhance the LLM's understanding of the issue's root cause and retrieve context via iterative search; spectrum-based fault localization sharpens the context further, but only as long as a test suite is available.
- The reported result is 19% efficacy on SWE-bench-lite, 300 real-life GitHub issues, which the authors state exceeds the recently reported efficacy of SWE-agent.
- Cost is reported as a separate axis of the result: an average of $0.43 USD per issue, which the authors describe as significantly lower than other baselines.

## Notes

Two of the paper's mechanisms carry stated conditions. Spectrum-based fault localization applies
only where a test suite is available, and the comparison against SWE-agent is against that system's
efficacy as recently reported rather than against a run the authors performed themselves. The
concluding claim — that the workflow enables autonomous software engineering in which auto-generated
code is itself autonomously improved — is posited by the authors as a prospect rather than
demonstrated by the reported experiments. The preprint went through three versions between April and
July 2024.
