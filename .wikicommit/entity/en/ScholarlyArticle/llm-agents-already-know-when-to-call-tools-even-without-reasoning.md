---
title: "LLM Agents Already Know When to Call Tools - Even Without Reasoning"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, tool-use, benchmarks]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.09252'
    hash: sha256:7d08538d9f45eb05bc7d8ea511fcfef0aca596fc3189f3397a075cc61cb6838e
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A preprint from the University of California, San Diego that introduces the When2Tool benchmark for studying whether LLM agents call tools only when they need them, finds that tool necessity is linearly decodable from a model's pre-generation hidden states, and proposes Probe&Prefill to act on that signal."
  author: ["Chung-En Sun", "Linbo Liu", "Ge Yan", "Zimo Wang", "Tsui-Wei Weng"]
  abstract: "Tool-augmented LLM agents tend to call tools indiscriminately, even when the model can answer directly. The paper proposes When2Tool, a benchmark of 18 environments spanning three categories of tool necessity with controlled difficulty levels, shows that prompt-only and reason-then-act baselines give limited control, finds that tool necessity is linearly decodable from pre-generation hidden states with AUROC 0.89–0.96 across six models, and proposes Probe&Prefill, which reduces tool calls by 48% with 1.7% accuracy loss."
  keywords: ["tool-call decisions", "tool necessity", "linear probing", "prefilling", "LLM agents"]
---

This preprint studies a single decision inside [[DefinedTerm/agentic-tool-use]]: whether an agent
should call a tool at all or answer directly. The authors start from the observation that
tool-augmented agents tend to call tools indiscriminately, and that each unnecessary call costs API
fees and latency, while existing tool-use benchmarks assume every task needs a tool. They ask whether
models overcall because they lack the information to decide, or because they fail to act on
information they already have.

To study the question they build [[Dataset/when2tool]], a benchmark whose tasks run from ones a model
can usually solve directly to ones that are impossible without a tool, and evaluate six open models
(Qwen3-1.7B/4B/14B/32B and Llama-3.1-8B/3.3-70B) under two families of training-free baselines:
Prompt-only, which varies the system prompt from "tool use is mandatory" to "do not use any tools",
and Reason-then-Act, which asks the model to reason about whether it needs a tool before acting.
They then train a linear probe on the hidden state at the last input token to predict whether a tool
call is necessary.

Building on that probe, the paper proposes Probe&Prefill. At inference time the probe reads the
hidden states from the ordinary prompt-encoding forward pass, compares its probability with a
threshold τ, and prefills the start of the model's response with a short steering sentence — "I can
solve this directly without using a tool." or "I need to use a tool for this question." — from which
the model continues generating. The threshold is a single knob for trading accuracy against tool
calls, and the method needs no fine-tuning and no extra reasoning tokens.

## Key Points

- Under the default prompt, models make 2,100–4,400 tool calls across the 2,250 single-hop test
  tasks — more than one call per task — and even on easy tasks Qwen3-1.7B makes 864 calls across 750
  tasks; the authors characterise the default behaviour as "tools are available, therefore use them".
- Prompts that discourage tool use reduce calls indiscriminately, including on hard tasks where tools
  are genuinely needed: on Qwen3-4B-Instruct, the accuracy cost per saved call when moving from the
  default to the "sparse" prompt is −17.3 on easy tasks but −42.4 on hard ones.
- Reason-then-Act only partly helps, adds generated tokens, and is model-dependent: on Llama-3.1-8B
  accuracy fell from 79.5% to 31.2% and on Llama-3.3-70B from 83.1% to 47.9%, because the models
  narrated an intent to call a tool without producing a valid call.
- Neither baseline can target a tool-call budget: each prompt mode gives one fixed operating point,
  and several of those points are nearly indistinguishable.
- Tool necessity is linearly decodable from pre-generation hidden states, with probe AUROC of
  0.89–0.96 across the six models, and the signal is present even for the Llama models whose
  reason-then-act generation collapses — which the authors read as models already knowing when a
  tool is needed but failing to act on it.
- Across all models tested, Probe&Prefill reduces tool calls by 48% with 1.7% accuracy loss, while
  the best baseline at comparable accuracy reduces them by only 6%, or reaches a similar reduction
  with five times the accuracy loss.
- On the Search-o1 agentic search benchmarks, evaluated with Qwen3-4B-Instruct only, Probe&Prefill
  reduced search API calls by 20–56% without accuracy degradation on most datasets; MuSiQue was the
  exception, where the best baseline achieved a larger reduction.
- The probe adds under 0.7 ms per task across the six models, and full supervised fine-tuning,
  tested as a stronger baseline on three models, improved accuracy by 2–3% but did not reliably reduce
  tool calls.

## Notes

The Reason-then-Act baseline is described as inspired by the think-before-act paradigm of
[[ScholarlyArticle/react-synergizing-reasoning-and-acting]] and Reflexion. The authors position the
work against prior efficiency methods that fine-tune a model or iteratively optimise instructions and
tool descriptions without first asking why models overcall, and against probing work that steers
models by modifying activations or weights: Probe&Prefill steers through the output prefix instead,
so it leaves the forward pass unchanged.

Soft prefill lets the model override the steering sentence. On the Llama models the authors report
that it is partly ignored because of weak instruction following, and a hard-prefill mode that forces
the output format restores control of the trade-off there. Additional experiments cover multi-hop
tasks, transfer of the probe to held-out environments within the same category, and ablations of
layer selection, temperature, training-data size and regularisation. The extracted version is
arXiv:2605.09252v2, marked as a preprint.
