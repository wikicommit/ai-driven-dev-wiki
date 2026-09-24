---
title: "The Bitter Lesson of Tool Calling"
type: "schema:ScholarlyArticle"
lang: en
tags: [tool-use, agents, benchmark, empirical-study]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2608.06370'
    hash: sha256:dec66d23f3c920237899e23a098559303cf1572e36040c7738b274d516b55dd4
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A PricewaterhouseCoopers study comparing programmatic tool calling with native JSON tool calling across 14 language models on BFCL v4, with ablations on sequential chaining, parallel fan-out and context flooding."
  author: ["Ishan Patel", "Sahil Sen", "Elias Lumer", "Vamse Kumar Subbiah"]
  abstract: "Programmatic tool calling replaces rigid JSON tool calls with scripts that chain and parallelise naturally: tools are exposed as typed Python stubs that the model invokes through code, with execution and results handled in a single agent turn. The paper compares it with native JSON tool calling across 14 language models on BFCL v4. Programmatic tool calling matches or exceeds JSON tool calling in 11 of 14 models, with the GPT-5.6 family improving 10.6% over its JSON baseline; it matches or outperforms the baseline in 13 of 14 models under parallel fan-out, and holds stable under context-rot conditions where the baseline degrades 2.3% on average."
  keywords: ["programmatic tool calling", "JSON tool calling", "function calling", "BFCL v4", "context rot"]
---

This paper, by four authors at PricewaterhouseCoopers' Commercial Technology and Innovation Office,
tests whether [[DefinedTerm/programmatic-tool-calling]] can replace native JSON tool calling
without losing accuracy. It frames prior work, including [[DefinedTerm/codeact]], as having made
the case for executable code over JSON tool calls without evaluating the two on a standardised
benchmark across model families, and it picks function calling as the harder test case because it
requires precise argument serialisation, multi-step chaining and fan-out across heterogeneous APIs.

The evaluation uses a 309-entry representative subset of
[[Dataset/berkeley-function-calling-leaderboard]] v4 spanning eight task categories, scored by a
deterministic comparison of the calls made against ground truth, and 14 models from Anthropic and
OpenAI released between November 2024 and July 2026, all run at temperature 0. In the programmatic
condition the model receives the source of a typed Python stub module compiled from the benchmark's
function schemas and writes one script that the agent loop executes in a shell subprocess; a stop
middleware then ends the loop, so both paradigms consume the same number of LLM calls per entry.
Three ablations target the task structures where JSON tool calling's limitations are most often
claimed: sequential chaining (52 entries, chain lengths 2–20), parallel fan-out (32 entries, 7–48
calls, plus probe entries up to 100) and [[DefinedTerm/context-rot]], in which decoy function
schemas from unrelated domains flood the context to 128 schemas (31 entries per condition).

## Key Points

- On the main BFCL v4 subset, programmatic tool calling matched or exceeded JSON tool calling in 11
  of 14 models; GPT-5.6-Sol and GPT-5.6-Terra each improved 10.6 points over their own JSON baseline.
- The authors report that viability followed model generation rather than model family: all five
  Anthropic models and the three newest GPT-5.6 variants matched or exceeded the baseline, while
  GPT-4o, GPT-4.1 and GPT-5.4-mini fell 19.7–26.9 points below it. For those three the failure was
  consistent — they wrote literal `\n` escape sequences instead of real newlines, so any multiline
  script failed with a syntax error.
- In the chaining ablation Claude Sonnet 5 gained most (80.8% to 96.2%), followed by Claude Opus 4.8
  (80.8% to 94.2%), while GPT-4.1 collapsed from 98.1% to 40.4% because of the same newline failure.
  Programmatic tool calling completed chaining entries in roughly half the wall-clock time of the
  baseline for 13 of 14 models, since JSON tool calling needs an extra inference turn per step;
  GPT-5 was the exception at 2.8 times baseline latency.
- In the parallel fan-out ablation it matched or exceeded the baseline for 13 of 14 models, with
  GPT-5 rising from 71.9% to 96.9%. Probing Claude Sonnet 5, JSON enumeration accuracy was 100% up
  to 70 calls, 75% at 72 and 0% at 100, while programmatic tool calling held 100% at 72 and 100;
  GPT-5.6-Sol held 100% under JSON through 100 calls, so the authors attribute the limit to how
  Anthropic models serialise parallel tool-call blocks rather than to JSON tool calling in general.
- Under context flooding the mean change from filtered to flooded context was −2.3 points for JSON
  tool calling and +5.5 for programmatic tool calling; a filesystem-based discovery condition,
  included only as an internal reference point, fell 32.0 points.
- Token costs crossed over at about 26 fan-out calls: below that, programmatic tool calling cost
  more because of its fixed system-prompt overhead, and on the chaining ablation it used 1.5 times
  the input tokens of JSON tool calling.
- Several models answered aggregation questions from parametric knowledge without executing the
  enumeration calls, so the authors treat enumeration accuracy as the primary measure of whether
  the tools were actually invoked.

## Notes

Averaged across all 14 models, programmatic tool calling was 14.1 points below JSON tool calling in
the parallel and parallel_multiple categories and 10.0 points above it in live_multiple, a
parallel-category gap the authors attribute largely to the three OpenAI models with the newline
failure. They state four limitations: the benchmark's stubs echo their arguments rather than
executing real APIs, so the study measures argument serialisation rather than end-to-end tool use
where return values feed later calls; the ablations are small (31–52 entries) and individual model
results are directional; the benchmark's ground-truth labels may carry noise; and programmatic tool
calling carries a fixed input-token overhead. The abstract and conclusion give the GPT-5.6 family's
main-evaluation gain as 10.6% and 10.7% respectively.
