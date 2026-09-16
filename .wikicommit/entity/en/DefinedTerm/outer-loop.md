---
title: "Outer Loop"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/own-the-outer-loop/'
    hash: sha256:4945c6720401f08dd3c43a7ec8fd0b79a1c8eb6f08bfa4b0da49f6e4a0c6173a
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "As framed in Addy Osmani's 'Own the Outer Loop' keynote, the part of an agentic engineering workflow that a human retains ownership of — deciding what should be built, setting the constraints it runs under, reviewing the evidence it produces, and being answerable for the result — while an agent runs the 'inner loop' of investigating, implementing, and verifying the task itself."
---

In his "Own the Outer Loop" keynote, Addy Osmani frames the outer loop as the part of an agentic coding workflow that a human retains ownership of, distinguished from the "inner loop" that a coding agent runs on its own: investigating a task, implementing a plan, and verifying the result. Where the inner loop is a matter of capability — what a model plus its harness can do — the outer loop is a matter of agency: deciding what should be built, verifying that it was built safely, approving it, and owning the outcome. The claim is that agents have moved from assisting inside the inner loop to running the entire inner loop themselves, which is what makes owning the outer loop the part of the work that is left for engineers.

## Usage

Osmani organizes the outer loop around three terms he names in the keynote: Quality, the checks installed before a system is allowed to run, which produce evidence; Verdict, the production decision made from that evidence — ship, block, redirect, narrow the response, add a guardrail, or reject outright; and Answerability, the guarantee that the person who made the Verdict can explain it if asked. He frames the human's role as not needing to be inside the inner loop to hold the outer loop, occupying instead four narrower loops he names: the constraints loop (what inputs, architectures, instructions, or invariants to set), the sampling loop (how much output to sample and review), the audit loop (what evidence to keep and whether the audit log is effective), and the ownership loop (which part of the production boundary a given person owns).

## When It Applies

It applies once agents are trusted to run the inner loop unattended, at a scale or speed a human could not review turn by turn — the post cites survey evidence that a large and growing share of committed code is AI-generated or AI-assisted, and separate research showing that review and governance have become the bottleneck, typically arriving only after code has already been created and the risk already accepted. It assumes a back-pressure mechanism — ordinary engineering signals such as type checks, tests, hooks, sandbox limits, audit logs, and monitors — that constrains how much autonomy an agent is actually granted, deliberately less than the maximum autonomy it could exercise. Skipping it is described as producing three hidden costs: cognitive surrender, cognitive debt, and the orchestration tax.

## Related Terms

[[DefinedTerm/loop-engineering]], [[DefinedTerm/harness-engineering]], [[DefinedTerm/cognitive-surrender]], [[DefinedTerm/cognitive-debt]], [[DefinedTerm/orchestration-tax]]
