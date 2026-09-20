---
title: "StruQ: Defending Against Prompt Injection with Structured Queries"
type: "schema:ScholarlyArticle"
lang: en
tags: [llm, security, prompt-injection, agent-safety, evaluation]
sources:
  - type: url
    url: 'https://www.usenix.org/system/files/usenixsecurity25-chen-sizhe.pdf'
    hash: sha256:91f97972f9337ec68915889ea729157686ff67d4a51b175b55127f2e715de659
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A USENIX Security 2025 paper proposing structured queries as a defense against prompt injection, and StruQ, a system combining a secure front-end with a structured-instruction-tuned LLM that reduces all tested manual attacks to under 2% success with little or no utility loss."
  author: "Sizhe Chen, Julien Piet, Chawin Sitawarin and David Wagner"
  datePublished: "2025-08-13"
  keywords: [prompt injection, LLM-integrated applications, instruction tuning, structured queries, adversarial robustness]
---

This paper, from four UC Berkeley authors and presented at the 34th USENIX Security Symposium,
addresses prompt injection in LLM-integrated applications — which it notes OWASP has dubbed the
number one security risk for LLM applications. Its diagnosis is structural: existing LLMs offer an
unsafe-by-design API in which the application concatenates the developer's prompt and untrusted
data into a single string, and the model, scanning its whole input for instructions to follow,
cannot tell one part from the other.

Its proposal is [[DefinedTerm/structured-query]], a general approach in which the prompt and the
data are supplied to the model as two separate channels. Because training an entirely new LLM from
scratch is impractical, the authors build a system, StruQ, that realises structured queries on top
of an existing base (non-instruction-tuned) model. StruQ has two components: a secure front-end
that encodes a prompt and data into a special format using reserved delimiter tokens and filters
those tokens out of the user data, and an LLM converted by [[DefinedTerm/structured-instruction-tuning]]
to follow instructions only in the prompt portion of that encoded input.

The authors evaluate StruQ against at least 15 prompt-injection attack techniques on Llama-7B and
Mistral-7B, and report that it decreases the success rate of all tested manual attacks to under 2%
while imposing little or no loss of utility as measured by AlpacaEval. They are explicit that the
result is a first step rather than a finished defense: optimization-based attacks remain
non-trivially effective, and they call defending against them an important open research problem.

## Key Points

- Prompt injection is presented as the latest instance of a decades-old vulnerability pattern —
  control and data sent over the same channel — with the paper tracing the same shape through the
  2600 Hz payphone tone attack, SQL injection, cross-site scripting and command injection, and arguing
  that in each case the robust solution has been to separate the two, as SQL prepared statements
  do.
- The paper distinguishes prompt injection from jailbreaking by the number of parties: jailbreaking
  is a two-party setting (trusted model provider, untrusted user), while prompt injection is a
  three-party one (trusted model provider, trusted application developer, untrusted source of user
  data) in which the attacker chooses data that violates the developer's security goals. Its
  consequence is that general safety tuning or filtering designed to stop jailbreaks cannot catch
  prompt injection.
- The paper's threat model assumes the attacker can arbitrarily modify the data portion of a query
  but not the prompt, and knows both the prompt and the application's formatting. An attack counts
  as successful if the response obeys the hidden instruction rather than treating it as data.
- The authors highlight [[DefinedTerm/completion-attack]]s as a powerful and under-addressed family,
  and state they are the first to propose a defense that takes them into account in both method
  design and evaluation.
- Against undefended models, Completion-Real reaches 96% attack success on both Llama and Mistral;
  StruQ reduces it to 0% on both. Reported across the manual attack table, StruQ's highest measured
  success rate on either model is 2%.
- StruQ also improves robustness against two optimization-based attacks it was never trained on:
  on Llama, Tree-of-Attacks-with-Pruning falls from 97% to 9% and Greedy Coordinate Gradient from
  97% to 58%. The authors credit those attacks' remaining strength to their generating
  task-specific injections — they report 68% of the TAP injections generated against the StruQ
  models had a close semantic connection to the original instruction — and note both are more than
  100x more expensive in GPU hours than the other attacks tested.
- Utility is measured with AlpacaEval 1.0 over 805 AlpacaFarm samples. The Llama model goes from
  67.2% to 67.6% and the Mistral model from 80.0% to 78.7%; with AlpacaEval's standard error of
  0.7%, the authors describe the Mistral reduction as borderline statistically significant at the
  0.05 level and the Llama change as not statistically significant.
- Compared directly against BIPIA, a training-time defense the authors reproduce on Vicuna-7B,
  StruQ is reported as both more secure and less costly to utility: attacks reach 0% against the
  StruQ model on both test sets with no utility loss, while BIPIA leaves a 54% Ignore-attack
  success rate on StruQ's test set and drops AlpacaEval win rate from 53.9% to 26.0%. GCG succeeds
  against BIPIA at a 100% rate.
- The authors state four limitations of StruQ's scope: it protects only programmatic applications
  that invoke LLMs through an API or library and not web-based multi-turn chatbots, because end
  users are unlikely to mark which parts of their conversation are instructions and which are data;
  it is not designed to defend against jailbreaks, data extraction or other attacks; it is not a
  completely secure defense in the worst case; and further research is needed against
  optimization-based attacks.

## Notes

The paper's recommendation to model providers follows from its own construction: because defenses
against prompt injection build on top of non-instruction-tuned models, it encourages LLM providers
to make non-instruction-tuned models available for fine-tuning. Its suggested future directions
include access control and rate-limiting to detect and ban iterative attackers, novel architectures
inherently robust to prompt injection — the authors float masking attention between the prompt and
data portions in initial layers — and extending the structure to include a system prompt alongside
the user prompt and the associated data.
