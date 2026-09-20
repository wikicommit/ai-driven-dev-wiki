---
title: "How Do AI Coding Agents Contribute to Software Development? an Empirical Study of Agentic Pull Requests"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, software-engineering, pull-requests]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2607.21832'
    hash: sha256:70d1d2ef164750a4378fe8bae762c51bfeb9b16474147766f2c6ddacf2524c02
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "A longitudinal empirical study using the AIDev dataset that characterizes agent-authored pull requests against human-generated ones, tracking how merge rates, task types, and pull request characteristics change across stages of the development lifecycle."
  author: ["Iren Mazloomzadeh", "Mohammad Mehdi Morovati", "Foutse Khomh"]
  datePublished: "2026-07-23"
  keywords: ["Software Engineering", "Machine Learning"]
  citation: "arXiv:2607.21832"
---

This study sets out to characterize agentic pull requests — those authored by AI coding agents — in
comparison with human-generated pull requests, and to examine how their properties change across
different stages of the software development lifecycle. The authors' premise is that while
developers increasingly benefit from coding agents, the agents' impact on software quality remains
insufficiently understood, and that how agentic contributions evolve across the lifecycle has not
been thoroughly investigated.

The analysis is built on the [[Dataset/aidev]] dataset. Working from it, the authors first analyze
how differences in merge rates between agentic and human-generated pull requests vary over time.
They then identify the types of development task to which AI coding agents are predominantly
applied, and investigate how those task distributions evolve across development quarters. Finally
they compare a set of key characteristics of agentic and human-generated pull requests, with
attention to what those characteristics imply for software quality and to how they change over
time.

The authors present the contribution as an empirical and longitudinal perspective on the role of AI
coding agents in software development, offering what they describe as a more nuanced understanding
of the benefits and limitations of these agents in real-world practice.

## Key Points
- Characterizes agentic pull requests against human-generated ones and tracks how their properties
  change across stages of the software development lifecycle
- Uses the AIDev dataset as its material
- Analyzes how merge-rate differences between agentic and human-generated pull requests vary over
  time
- Identifies the development task types AI coding agents are predominantly applied to, and how
  those task distributions evolve across development quarters
- Compares key characteristics of the two kinds of pull request with respect to their implications
  for software quality

## Notes

The paper is positioned as longitudinal — its distinguishing move is tracking change over
development quarters rather than taking a single snapshot. Its authors present the contribution as
a more nuanced understanding of the benefits and limitations of coding agents in real-world
practice, rather than as a verdict on their impact on software quality.
