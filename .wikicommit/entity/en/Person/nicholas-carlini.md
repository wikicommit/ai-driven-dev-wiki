---
title: "Nicholas Carlini"
type: "schema:Person"
lang: en
tags: [researcher, agent-harness, security]
sources:
  - type: url
    url: 'https://www.anthropic.com/engineering/building-c-compiler'
    hash: sha256:76ec31b147cb595b08d33f9b46ece5a385276d3165f3c8ca4ab62600055ab111
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A researcher on Anthropic's Safeguards team who stress-tests the limits of what language models can achieve, and who previously worked in penetration testing."
  affiliation: "[[Organization/anthropic]]"
  jobTitle: "Researcher"
  birthDate: ""
---

Nicholas Carlini is a researcher on the Safeguards team at [[Organization/anthropic]]. His stated method is to push language models to their limits and study where they begin to break down, on the reasoning that this is the best way to understand what they can do.

## Background

The source available here records that he previously worked in penetration testing, exploiting vulnerabilities in products produced by large companies — a background he invokes when explaining why autonomous software development makes him uneasy, since it makes the prospect of programmers deploying software they have never personally verified a concrete rather than abstract concern.

## Works & Achievements

He built and reported the parallel agent-team experiment described in [[BlogPosting/building-a-c-compiler-with-parallel-claudes]], in which 16 agents produced a 100,000-line Rust C compiler capable of building Linux 6.9. He describes using that C compiler project as a recurring capability benchmark across the Claude 4 model series, drafting the same specification each time — a from-scratch optimising compiler with no dependencies, GCC-compatible, able to compile the Linux kernel, and designed to support multiple backends — while deliberately leaving the implementation approach unspecified.
