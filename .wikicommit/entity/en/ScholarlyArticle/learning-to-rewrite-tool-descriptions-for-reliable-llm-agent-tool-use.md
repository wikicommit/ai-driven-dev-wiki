---
title: "Learning to Rewrite Tool Descriptions for Reliable LLM-Agent Tool Use"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, tool-use, fine-tuning]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2602.20426'
    hash: sha256:0dc3bb1680522eb9a064b913e587250e0df63f198c995e181cdc64487d6286ee
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A preprint proposing Trace-Free+, a curriculum-learning framework that trains a model to rewrite tool descriptions from the tool schema alone, so that LLM agents select and call unseen tools more reliably, especially in large tool catalogs and multi-step tasks."
  author: ["Ruocheng Guo", "Kaiwen Dong", "Xiang Gao", "Kamalika Das"]
  abstract: "The paper argues that LLM tool-using agents increasingly plateau because of the quality of the tool interfaces they consume, and proposes Trace-Free+, a curriculum learning framework that progressively transfers supervision from trace-rich settings to trace-free deployment. Supported by a large dataset of tool interfaces derived from real-world APIs, it improves robustness as tool catalogs scale past 150 candidates, generalizes across domains without retraining, and adds gains on top of agent fine-tuning."
  keywords: ["tool descriptions", "tool use", "curriculum learning", "LLM agents"]
---

This preprint from Intuit AI Research targets the interface side of [[DefinedTerm/agentic-tool-use]].
Its starting argument is that most efforts to improve tool-using agents change the agent — larger
models, better prompting or fine-tuning — while the tool descriptions the agent reads are typically
written for human developers: they tolerate ambiguity, leave constraints implicit and assume
background knowledge an agent cannot acquire, and these deficiencies compound as the number of
candidate tools grows. Existing methods that improve tool descriptions either re-run a per-tool
pipeline of query synthesis, trajectory collection and annotation for every new API, or rewrite each
tool independently, so they cannot learn patterns that transfer to unseen tools.

The authors' hypothesis is that effective tool descriptions follow a bounded, reusable set of
interface patterns, and that rewriting descriptions can therefore be learned as a transferable
capability. Their method, Trace-Free+, fine-tunes a small open-weight model (Qwen3-4B-Instruct) to
generate an improved description from a tool's original interface. Training follows a curriculum:
it begins with a higher share of examples that include a summary of execution traces and shifts
toward examples with no traces, matching deployment conditions in which a new tool arrives with only
its schema. The training targets come from a three-stage pipeline over real-world RESTful APIs drawn
from ToolBench — annotating working tools with an agentic prober, synthesizing multi-step queries
with inter-call dependencies, and refining descriptions first with general documentation guidelines
and then with rules extracted from failed trajectories.

Evaluation holds out every test tool from training. The main benchmark is StableToolBench, with
cross-domain transfer tested on RestBench (TMDB and Spotify) and on
[[Dataset/berkeley-function-calling-leaderboard]] v2, using GPT-4.1 as the primary tool-using agent.

## Key Points

- The paper identifies five categories of interface pattern that effective descriptions share: tool
  selection scope (when to use a tool and when not to), cross-tool dependencies, output description,
  parameter constraints, and cross-parameter dependencies. Original descriptions covered fewer than
  12% of the analysed tools in any category, while Trace-Free+ reached 97.2% for tool selection scope
  and 94.2% for parameter constraints.
- On multi-step StableToolBench queries, Trace-Free+ reached 44.6% query-level success against 33.5%
  for the original descriptions and 41.5% for descriptions rewritten with general guidelines; on
  single-step queries it did not beat the guideline-based rewrite (60.7% against 61.6%).
- In scaling experiments that expose the agent to 150 or more candidate tools, Trace-Free+ reduced
  the accuracy degradation of the original descriptions by 29.23% and improved query-level success by
  60.89% on average — the largest gains in the evaluation, which the authors read as interface
  optimization mattering most when tool catalogs are large.
- The rewritten descriptions transferred to RestBench with up to 51.3% relative improvement in
  query-level success on TMDB over the original descriptions, and improved GPT-4.1, Claude Sonnet 4.5
  and Gemini-3-pro-preview on BFCL v2 without any change to those agents.
- Description rewriting and agent fine-tuning were complementary: with a Qwen3-4B-Instruct agent on
  RestBench, fine-tuning alone moved query-level success from 54.1% to 55.0%, Trace-Free+ alone to
  62.1%, and the two combined to 62.9%.
- The authors' deployment advice is that guideline-based rewriting suffices for simple queries and
  small catalogs, while Trace-Free+ suits large tool catalogs with multi-step workflows.

## Notes

The evaluation introduces step-wise teacher forcing, in which the ground-truth tool is executed at
each step regardless of the agent's choice, so that a failure can be attributed to the agent's
reading of the current tool's description rather than to earlier mistakes; the scaling experiments
instead execute the agent's own choices. The authors also corrected a subset of StableToolBench
parameter schemas that did not match what the servers required, and evaluated all methods on the
corrected schemas, so their absolute numbers are not directly comparable with work that uses the
original schemas.

Limitations the authors state include the single-step gap noted above, which they attribute to
synthesized training queries averaging three tools; the use of one small base model as the
description generator; and the difficulty of measuring the precision of inferred constraints, since
the model may occasionally hallucinate constraints — such as value ranges the server does not
enforce — for unfamiliar APIs. The paper is marked as a preprint under review; the version extracted
here is arXiv:2602.20426v2.
