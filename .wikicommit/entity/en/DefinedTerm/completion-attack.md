---
title: "Completion Attack"
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
  description: "A family of prompt injection attacks that append a fake response to the prompt so the model believes the application's task is already finished, then inject new instructions behind the appropriate delimiters."
---

A Completion attack is a prompt injection technique that first appends a fake response to the
prompt, misleading the LLM into thinking the application's task has been completed, and then
injects new instructions, which the model tends to follow. Appropriate delimiters are inserted so
the injected text matches the format of legitimate queries. It is named and taxonomised in
[[ScholarlyArticle/struq]], whose authors describe their Completion attacks as inspired by earlier
work by Simon Willison, and who say they highlight the importance of Completion attacks in that
paper.

## Usage

The paper separates the family by which delimiters the attacker uses. A **Completion-Real** attack
uses exactly the same delimiters as a legitimate query, which it describes as the most effective
strategy; a **Completion-Close** attack uses slight variants of them, the paper's example being
"#Response" in place of "###response:"; and a **Completion-Other** attack uses some delimiter
entirely unrelated to the legitimate ones, drawn in the paper's evaluation from hundreds of
manually designed alternatives.
Two combined forms are also defined: **Completion-RealCmb** and **Completion-OtherCmb**, each
folding the Ignore and Escape-Separation techniques into the corresponding Completion attack.

Measured against undefended models, the family is the strongest of the paper's hand-crafted
attacks. Completion-Real reaches 96% attack success on both the Llama and Mistral baselines, and
the highest-scoring Completion-Close variant reaches 96% on both as well; Completion-Other reaches
29% on Llama and 71% on Mistral. Translating the injected instruction into Chinese or Spanish
leaves Completion-Real effective against the undefended models (66% and 50% on Llama, 96% and 92%
on Mistral), whereas base64-encoding the whole injection drops it to 0% on both.

The paper's defense addresses the family in two distinct places, which is why it is treated as a
design target rather than just another attack in a list. Attacks using the real delimiters are
stopped by the front-end's recursive filter, which removes the reserved delimiter tokens from user
data before the model sees it; attacks using near-miss delimiters are stopped by
[[DefinedTerm/structured-instruction-tuning]], because the real delimiters tokenize to reserved
tokens while near-miss ones tokenize as ordinary text. The authors state that StruQ stops all
Completion attacks they were able to design; the residual figures in their tables run up to 2%,
for Completion-RealCmb against the defended Mistral model. They also note that without the filter,
Completion attacks using the real delimiters would still be effective.

## Related Terms

[[DefinedTerm/prompt-injection]], [[DefinedTerm/structured-query]],
[[DefinedTerm/structured-instruction-tuning]]
