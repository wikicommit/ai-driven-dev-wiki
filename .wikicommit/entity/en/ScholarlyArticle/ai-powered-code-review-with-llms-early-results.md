---
title: "AI-powered Code Review with LLMs: Early Results"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, multi-agent, code-smells]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2404.18496'
    hash: sha256:2814a3d61744a6080c0eba56810e965df3e68fbbb55c5ecfb97f34bf9762da3a
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A short early-results paper proposing an LLM-based multi-agent system for code review in which four GPT-4 agents — code review, bug report, code smell and code optimization — identify bugs, code smells and deviations from coding standards and suggest improvements. Its evaluation is preliminary and qualitative."
  author: ["Zeeshan Rasheed", "Malik Abdul Sami", "Muhammad Waseem", "Kai-Kristian Kemell", "Xiaofeng Wang", "Anh Nguyen", "Kari Systä", "Pekka Abrahamsson"]
  keywords: ["Generative AI", "Large Language Model", "Software Engineering", "OpenAI", "Artificial Intelligence", "Code Reviews"]
---

The paper argues that traditional code review processes and static analysis tools often lack the depth to give actionable feedback beyond detecting syntax errors or known bug patterns, and that there is no LLM-based model specifically designed to enhance code review by identifying issues, suggesting optimizations and educating developers on best practices. It surveys earlier automation of code review — reviewer recommendation, predicting whether a change will be approved, retrieval-based comment recommendation, and Transformer models that revise code to meet review comments — and concludes that a comprehensive LLM-based tool for detailed review is missing.

The proposed system has four agents built with prompt-based instructions on GPT-4, each handling one aspect of review and passing its findings on through a centralized coordination component. A Code Review Agent makes the initial assessment, looking for bugs, code smells and deviations from coding standards; a Bug Report Agent performs a more targeted inspection for potential bugs; a Code Smell Agent makes a design-oriented evaluation and proposes refactoring strategies to reduce technical debt; and a Code Optimization Agent suggests changes to algorithms, redundancy and efficiency and can produce optimized versions of the code while preserving its functionality. The authors frame the goal as a dual benefit: better code quality and developer learning about best practices, and they present the system's proactive approach to code improvement as a step forward from traditional static analysis tools.

## Key Points

- The authors report that in preliminary evaluation the system autonomously reviewed source code and produced logical, actionable feedback across all four agent roles, identifying issues from minor bugs to significant code smells and inefficiencies across different programming languages and AI application domains.
- They report that the bug-detection agent found logical inconsistencies, potential runtime errors and error-prone structures, in several cases catching issues that traditional static analysis tools missed or explained only briefly.
- They report that the code smell agent's refactoring suggestions were generally aligned with accepted software engineering principles, such as improving naming conventions, function decomposition and architectural clarity.
- These results are described qualitatively: the paper gives no benchmark, dataset, metrics or comparison, and defers accuracy and efficiency measurement to a planned empirical study with developers.

## Notes

The paper is positioned as early results. Planned future work includes comparing the system's output against manual methods, studying its educational effect on developers, and extending it into a multi-agent system that identifies a wide range of technical debt — code, design, architecture, testing, documentation, build and infrastructure debt. The work was funded by Business Finland. For a broader account of LLM-based review research, see [[ScholarlyArticle/a-roadmap-for-modern-code-review]] and [[DefinedTerm/code-review-agent]].
