---
title: "SWE-bench: Can Language Models Resolve Real-World GitHub Issues?"
type: "schema:ScholarlyArticle"
lang: en
tags: [evaluation, agents, llm, coding-agents, software-engineering]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2310.06770'
    hash: sha256:706b494065faa4145cd8f13923309b0192bd91ae7eac0d5f62df2ceaacb70416
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "The arXiv preprint that introduces SWE-bench, an evaluation framework of 2,294 software engineering problems drawn from real GitHub issues and pull requests across 12 Python repositories, in which a language model must edit a codebase to resolve a described issue."
  author: ["Carlos E. Jimenez", "John Yang", "Alexander Wettig", "Shunyu Yao", "Kexin Pei", "Ofir Press", "Karthik Narasimhan"]
  datePublished: "2023-10-10"
  abstract: "The paper argues that real-world software engineering is a rich, sustainable and challenging testbed for evaluating language models, and introduces SWE-bench, an evaluation framework of 2,294 software engineering problems drawn from real GitHub issues and corresponding pull requests across 12 popular Python repositories. Given a codebase and a description of an issue to resolve, a model must edit the codebase to address it — which frequently requires coordinating changes across multiple functions, classes and files, interacting with execution environments, processing extremely long contexts and reasoning beyond traditional code generation. The authors report that state-of-the-art proprietary models and their fine-tuned SWE-Llama resolve only the simplest issues, with the best-performing model, Claude 2, solving 1.96% of them."
---

This arXiv preprint introduces [[Dataset/swe-bench]], an evaluation framework built from real
software engineering work. The authors' framing is that language models have outpaced our ability to
evaluate them effectively, and that studying the frontier of their capabilities is essential to
their future development; they propose real-world software engineering as a rich, sustainable and
challenging testbed for the next generation of models.

SWE-bench consists of 2,294 software engineering problems drawn from real GitHub issues and the
corresponding pull requests, across 12 popular Python repositories. The task it poses is stated
directly: given a codebase along with a description of an issue to be resolved, a language model is
tasked with editing the codebase to address the issue. The authors argue this asks for more than
traditional code generation — resolving issues in SWE-bench frequently requires understanding and
coordinating changes across multiple functions, classes and even files simultaneously, calling for
models to interact with execution environments, process extremely long contexts, and perform complex
reasoning.

The reported results are low. Both state-of-the-art proprietary models and the authors' own
fine-tuned model, SWE-Llama, can resolve only the simplest issues, and the best-performing model,
Claude 2, is able to solve a mere 1.96% of the issues. The authors present advances on SWE-bench as
steps towards language models that are more practical, intelligent and autonomous.

The paper is filed under Computation and Language (cs.CL), Artificial Intelligence (cs.AI) and
Software Engineering (cs.SE). It was first submitted on 10 October 2023 and last revised on 11
November 2024 as version 3, carries the arXiv-issued DOI 10.48550/arXiv.2310.06770, and appeared at
ICLR 2024. Data, code and a leaderboard are stated to be available at <https://www.swebench.com>.

## Key Points

- The paper introduces SWE-bench, an evaluation framework of 2,294 software engineering problems taken from real GitHub issues and their corresponding pull requests across 12 popular Python repositories.
- Its motivating claim is that language models have outpaced our ability to evaluate them effectively, and that real-world software engineering makes a rich, sustainable and challenging testbed.
- The task format is to give a model a codebase plus a description of an issue and require it to edit the codebase to resolve that issue.
- The authors argue the benchmark demands capabilities beyond traditional code generation: coordinating changes across multiple functions, classes and files at once, interacting with execution environments, processing extremely long contexts, and complex reasoning.
- The headline measured result is that the best-performing model, Claude 2, solves 1.96% of the issues, with both state-of-the-art proprietary models and the authors' fine-tuned SWE-Llama resolving only the simplest ones — a figure that dates from this version of the paper rather than describing the benchmark's difficulty for later models.

## Notes

The benchmark's scope is bounded in ways the abstract states plainly: the repositories are Python,
there are 12 of them, and the problems come from issues that already have corresponding pull
requests. The authors position the low solve rates not as a verdict on the models but as a measure
of headroom — advances on SWE-bench are framed as steps towards more practical, intelligent and
autonomous language models. The preprint went through three versions between October 2023 and
November 2024.
