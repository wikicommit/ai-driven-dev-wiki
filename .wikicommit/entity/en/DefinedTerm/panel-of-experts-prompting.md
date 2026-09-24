---
title: "Panel of Experts prompting"
type: "schema:DefinedTerm"
lang: en
tags: [prompt-engineering, prompting, code-review]
sources:
  - type: url
    url: 'https://aise.phodal.com/aise-code-review.html'
    hash: sha256:c66c9a026df66e7f4feae11ee51fd39f0d6479793176e5269c0d01403e7f9453
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A prompting technique in which the model is asked to reason as a panel of experts who put forward, critique and check one another's steps in a discussion, intended to keep an LLM from carrying a wrong line of reasoning through to its answer."
---

Panel of Experts prompting asks a language model to reason as a panel of several distinct experts who discuss a problem together — one puts an argument forward, the others critique and check it — before an answer is returned. As described in Phodal's chapter on AI-assisted code review, summarising Sourcery's write-up on the technique, it extends an earlier prompt inspired by the tree-of-thoughts approach, in which three experts each write down one step of their thinking, share it with the group and move on to the next step, with any expert who realises they have made a mistake dropping out; that earlier prompt is reported, at least anecdotally, to do better than [[DefinedTerm/chain-of-thought]] on reasoning tasks.

## Usage

The panel version replaces the step-by-step relay with the idea of a panel discussion, on the reasoning that LLM training data contains many such discussions. The problem it targets is that once an LLM starts down a wrong line of reasoning it tends to follow it to the end rather than notice the error; a panel of experts with different roles is more likely to introduce different viewpoints and arguments, which should lead to better reasoning and results.

[[SoftwareApplication/sourcery]] used it in code review to decide which docstrings a diff requires updating. Its opening prompt casts the model as a panel of three experts on code documentation, named Alice, Bob and Charles, who work step by step and critique one another's work. The closing prompt has one expert argue for updating a given docstring and the others critique the argument and decide whether the update is needed, keeping only significant updates directly related to the changed lines, and has the result returned as a JSON list.

## When It Applies

It is aimed at reasoning tasks where a single chain of reasoning can go wrong early and never recover, such as judging whether a code change makes a docstring stale. It assumes a task the model can split into steps and arguments that the panel can critique. Its support is thin: the improvement of the prompt it builds on is reported only anecdotally, and the chapter presents the panel variant through one vendor's use of it rather than any measured comparison.

## Related Terms

- [[DefinedTerm/chain-of-thought]]
- [[DefinedTerm/prompt-engineering]]
