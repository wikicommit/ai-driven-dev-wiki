---
title: "Open-Prompt-Injection"
type: "schema:SoftwareApplication"
lang: en
tags: [prompt-injection, security, benchmark, llm]
sources:
  - type: url
    url: 'https://github.com/liu00222/Open-Prompt-Injection'
    hash: sha256:895ba881a5e3affcbccc872b5e101c586ba2ff92c22fdd66c076d3bdf431138a
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "An open-source toolkit and benchmark for prompt injection attacks and defenses, letting a researcher assemble a target task, a model, an injected task and a defense and evaluate the result."
  applicationCategory: "Prompt injection research toolkit"
  operatingSystem: "Python (conda environment)"
  featureList: "Factory API for models, tasks, attackers, apps and evaluators; ASV evaluation; declarative experiment matrix with dry-run; DataSentinel injection detector; PromptLocate injection localization"
---

Open-Prompt-Injection is an open-source toolkit for [[DefinedTerm/prompt-injection]] attacks and
defenses, published under an MIT license. Its stated purpose is to let a researcher implement,
evaluate and extend attacks, defenses, and the LLM-integrated applications and agents they are run
against — and the repository is also described as providing a benchmark for prompt injection attacks
and defenses in LLMs.

The abstraction it works in is the pairing of a **target task** with an **injected task**: the
application is built around the task it is supposed to perform, and an attacker injects a different
one into the data the application processes. The README's worked example makes the target task
sentiment analysis over SST-2 and the injected task spam detection over an SMS spam dataset.

## Capabilities

The library is used through factory functions that assemble the pieces: `create_model` from a model
config, `create_task` for both the target and (with `for_injection=True`) the injected task,
`create_attacker` for the attack strategy, `create_app` to wrap a task and model with a named
defense, and `create_evaluator` to score the result. The reported metric is called **ASV**, which the
evaluator computes from the target-task responses, the injected-task responses and the attack
responses; the README uses the acronym without expanding it. Changing which defense, attack strategy
or target task is measured is a matter of swapping config files and the arguments to those factory
functions rather than editing code.

Model configuration is by JSON file under `configs/model_configs/`, with API keys filled in by the
user; the README names PaLM 2, Meta's Llama models and OpenAI's GPT models when explaining where to
obtain keys, and its detector and localizer examples load a Mistral config.

The full experiment set from the associated paper runs from `run.py`, which reads a declarative
matrix at `configs/experiment_matrix.json` — a different matrix can be supplied with
`--matrix-config`, and `--dry-run` validates paths and prints every command without starting model
processes. The runner tracks each child process directly and exits non-zero if any experiment fails.
Response archives carry a configuration fingerprint and are reused only when it matches the active
experiment, with older archives lacking that metadata still readable but producing a warning.

## Defense components

Two named defense components ship with the toolkit, each distributed as a fine-tuned checkpoint
downloaded separately.

**DataSentinel** is a prompt injection *detector*: a `DataSentinelDetector` built from a model config
with the fine-tuned checkpoint path, whose `detect` method is called on a prompt. **PromptLocate**
is a prompt injection *localizer*, loaded from a LoRA adapter, whose
`locate_and_recover(prompt, target_instruction)` returns both a recovered prompt and a localized
prompt — so the answer it gives is not only that an injection is present but where in the input it
is, under the section heading "Prompt Injection Localization".

The repository presents these as composable into a **defense pipeline**: DataSentinel first
determines whether the prompts are contaminated, and PromptLocate is applied for localization and
data recovery only when contamination is detected. The README states that more detectors, and code
for fine-tuning, will be released.

## Adoption & Ecosystem

The repository points to a set of slides on prompt injection, described as an extended version of a
presentation given at the Safer with Google Summit 2025, for background on the attack class itself.
Setup is via a conda environment created from the repository's `environment.yml`.
