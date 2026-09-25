---
title: "Infrastructure noise"
type: "schema:DefinedTerm"
lang: en
tags: [evaluation, benchmarks, agentic-coding]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/infrastructure-noise'
    hash: sha256:9b90b3bbedd0a21cb782473b01e46d26c615e6e342bfbc0dc3d3f8087925a2c6
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Variation in agentic coding benchmark scores that comes from the evaluation infrastructure — resource allocation and its enforcement, time limits, cluster health, API latency — rather than from the model being evaluated."
---

Infrastructure noise is the variation in an agentic coding evaluation's score that is caused by the infrastructure the evaluation runs on rather than by the capability of the model under test. [[Organization/anthropic]] sets out the idea in [[BlogPosting/quantifying-infrastructure-noise-in-agentic-coding-evals]]: because an agentic eval gives the model a full environment in which it writes programs, runs tests, installs dependencies and iterates over multiple turns, the runtime is "an integral component of the problem-solving process" rather than a passive container, so two agents with different resource budgets and time limits "aren't taking the same test." Static benchmarks, which score a model's output directly, do not have this property.

## Usage

The main source of the noise Anthropic measured is resource configuration. Container runtimes enforce resources through a guaranteed allocation and a separate hard limit at which the container is killed; when both are pinned to the same value, a momentary memory spike can kill a container that would otherwise have succeeded. On [[Dataset/terminal-bench]] 2.0, Anthropic reports that moving from strict enforcement of per-task specs to uncapped resources lowered infra error rates from 5.8% to 0.5% and raised success by 6 percentage points (p < 0.01). It distinguishes two regimes: up to about three times the per-task spec, extra resources mainly remove spurious failures and the score change stays within noise, while beyond that they let the agent succeed with resource-hungry strategies it could not otherwise use, so the limits change what the eval measures. A smaller version of the effect — 1.54 percentage points between 1x and 5x RAM — appeared on [[Dataset/swe-bench]], whose tasks are less resource-intensive.

Anthropic describes resources as only one of the hidden variables: time limits, cluster health, hardware specs, concurrency level and egress bandwidth can all influence the score, and it reports anecdotally that pass rates fluctuate with time of day, likely because API latency varies. Its conclusion is that agentic evals are end-to-end system tests by construction, so the boundary between "model capability" and "infrastructure behavior" is blurrier than a single benchmark score suggests. A model provider can dedicate hardware to shield its own eval infrastructure from this, which Anthropic notes external evaluators cannot easily do.

The practical consequence it draws is about reading leaderboards: until resource methodology is standardized, differences below 3 percentage points deserve skepticism until the eval configuration is documented and matched. Its recommended mitigation is for evals to specify both the guaranteed allocation and the hard limit per task, with the band calibrated so that scores at the floor and ceiling fall within noise of each other, and to report the multiplier used; for publicly shared coding evals it also suggests running at multiple times and on multiple days to average out noise.

## Related Terms

- [[DefinedTerm/pass-at-k]]
- [[DefinedTerm/agent-harness]]
- [[DefinedTerm/sandboxing]]
- [[DefinedTerm/data-contamination]]
