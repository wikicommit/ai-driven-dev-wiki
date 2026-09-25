---
title: "SpecRover"
type: "schema:SoftwareApplication"
lang: en
tags: [coding-agents, code-review, verification]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2408.02232'
    hash: sha256:11a685d857df7202abc79fb94c2c9f7d605a6905b47206c856a11b12b3234adb
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An LLM agent for autonomous program improvement, built on AutoCodeRover, that resolves GitHub issues by inferring specifications of intended behavior during code search and vetting candidate patches with a reviewer agent that explains its decisions."
  applicationCategory: "LLM agent for automated issue resolution and program repair"
  featureList: "Reproducer agent; context retrieval with function summaries of intended behavior; patching agent; reviewer agent judging patch and reproducer test; regression test check with retries; selection agent with stated reasons; evidence output (buggy locations and intended behaviors, reproducer test, reasons for approval or selection)"
---

SpecRover is an LLM agent that resolves software issues — bug fixes and feature additions described
in a GitHub issue — by first inferring what the code is supposed to do. The paper that introduces it,
[[ScholarlyArticle/specrover-code-intent-extraction-via-llms]], calls it a progeny of
[[SoftwareApplication/autocoderover]]: it was implemented on the AutoCodeRover codebase and reuses
its context retrieval APIs, adding function summary extraction, patch reviewing and patch selection.
The authors state that its source code and experimental artifacts are available on Zenodo, and
they identify SpecRover with AutoCodeRover-v2, which they have also packaged as a GitHub bot
offering one-click issue resolution.

## Capabilities

Given an issue statement and a codebase, SpecRover runs a sequence of LLM agents. A reproducer agent
writes a test that reproduces the reported fault. A context retrieval agent searches the codebase
through structure-aware APIs, and for every function it retrieves writes a short natural-language
summary of how that function should behave to meet the issue's requirements; it ends by deciding on
the buggy locations. A patching agent then modifies code at those locations, guided by the paired
function summaries.

A reviewer agent executes the reproducer test on the original and the patched program and, given
the results, the issue and the test, decides separately whether the patch and the test are correct,
with an explanation; rejected patches and tests are revised using this feedback. An accepted patch
is checked against the project's regression test suite, with the workflow retried up to a
predefined number of times if regressions appear, and when no candidate passes, a selection agent
picks one from the issue description and states its reason. Alongside the final patch, SpecRover
outputs the buggy locations with their intended behaviors, the reproducer test, and the reason the
patch was approved or selected, which the authors suggest can serve as a commit message or be kept
with the code to track future regressions.

## Adoption & Ecosystem

SpecRover supports multiple LLMs as backends; the paper's experiments use Claude 3.5 Sonnet as the
main model, switching to GPT-4o for a task only when the Claude API returns an error. Although it was
designed for GitHub issues in Python repositories, the paper demonstrates it on a C security
vulnerability in the Linux kernel from DARPA's AI Cyber Challenge, starting from a vulnerability
report. It belongs to the line of agents for [[DefinedTerm/software-issue-resolution]] and
[[DefinedTerm/automated-program-repair]].
