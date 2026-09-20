---
title: "Structured Instruction Tuning"
type: "schema:DefinedTerm"
lang: en
tags: [llm, security, prompt-injection, agent-safety]
sources:
  - type: url
    url: 'https://www.usenix.org/system/files/usenixsecurity25-chen-sizhe.pdf'
    hash: sha256:91f97972f9337ec68915889ea729157686ff67d4a51b175b55127f2e715de659
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A variant of instruction tuning that fine-tunes a base LLM on inputs carrying instructions in both the prompt and the data portion while training it to respond only to the former, so that the resulting model ignores instructions arriving in data."
---

Structured instruction tuning is a variant of instruction tuning that teaches a model to follow
instructions only in the prompt part of its input and not in the data part. It is introduced in
[[ScholarlyArticle/struq]], whose diagnosis is that standard instruction tuning is itself a core
contributor to prompt injection vulnerability: it trains an LLM to act on instructions found
anywhere in its input, no matter where they appear. The fix is to fine-tune on a mixture of normal
examples, which carry the instruction before the separator, and attacked examples, which carry
extra instructions after it, with the desired output in the second case being the response to the
correctly positioned instruction alone.

## Usage

The training set is built by augmenting a standard instruction tuning dataset. Half the samples are
left unchanged, to maintain the model's utility. A quarter are attacked with a Naive attack, the
sample's data portion having another training sample's instruction and data concatenated onto it,
with the desired response still the one belonging to the original prompt. The remaining quarter are
attacked with a Completion-Other attack, using fake delimiters drawn from a large collection that
does not overlap with the ones used in evaluation, and with a fake response whose text differs from
the true one — the paper notes that training on the true response instead teaches the model to
repeat its input. A sample with no data input is left unattacked, since prompt injection is only
relevant to applications that supply one.

The paper distinguishes this from traditional adversarial training: rather than using gradients to
craft worst-case adversarial examples, it simply concatenates another instruction from the training
set, which it describes as cheaper than approaches that rely on human-crafted malicious samples.
Deliberately, no manually designed malicious injections are needed, because the goal is only for
the model to answer the trusted instruction in the prompt part, which is guaranteed benign.

An ablation reported in the paper tests four augmentations — Naive, Ignore, Completion-Other and a
fake-delimiter augmentation that trains the model to reject when delimiters are wrong. The best
result comes from combining the Naive and Completion augmentations, which is reported as reducing
attack success to 0% across the selected attacks with minimal impact on utility, and is the
combination used in the final framework. The Ignore augmentation is reported as more effective than
the Naive one alone but as decreasing utility, and the fake-delimiter augmentation as causing the
model to reject some clean samples, lowering utility while failing to protect against most attack
types.

## When It Applies

The technique is applied to a base, non-instruction-tuned LLM: the paper converts one into a
structured-instruction-tuned model, and states that defenses against prompt injection build on top
of non-instruction-tuned models — which is why it encourages LLM providers to make such models
available for fine-tuning. In the paper's own runs it fine-tunes the whole model for three epochs
on a cleaned Alpaca instruction tuning dataset, at a learning rate of 2e-5 for Llama and 2.5e-6
for Mistral.

It assumes a companion front-end that encodes queries with reserved delimiter tokens and filters
those tokens out of the user data; the two are presented as parts of one system rather than as
independent measures. The paper's ablation on delimiters reports that special reserved tokens
matter to the outcome: after structured instruction tuning, Completion attacks using "near-miss"
delimiters are no longer effective, because correct delimiters encode to reserved tokens while
near-miss ones encode to ordinary text tokens whose different embeddings the tuned model has
learned to ignore. It also reports that initialising those new tokens' embeddings from the
corresponding ordinary text tokens makes a large difference to utility, and that instruction tuning
alone was insufficient for the model to learn an embedding for a new token from scratch. Its stated
limit is that the resulting model is not completely secure: optimization-based attacks retain
non-trivial success rates.

## Related Terms

[[DefinedTerm/structured-query]], [[DefinedTerm/prompt-injection]],
[[DefinedTerm/completion-attack]]
