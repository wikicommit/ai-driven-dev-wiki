---
title: "Introducing Devin, the first AI software engineer"
type: "schema:BlogPosting"
lang: en
tags: [agents, coding-agents, autonomous-agents]
sources:
  - type: url
    url: 'https://cognition.com/blog/introducing-devin'
    hash: sha256:73d2b8bef9a54736f9a6e7d6f3a7897727764c71d604e77c4ab4b9643a59d302
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Cognition's March 2024 launch post for Devin, which it calls the first AI software engineer: an agent that plans and carries out engineering tasks with its own shell, code editor and browser in a sandboxed environment. It reports a SWE-bench result for Devin evaluated unassisted, and announces early access through a waitlist."
  author: "Scott Wu"
  publisher: "[[Organization/cognition]]"
  datePublished: "2024-03-12"
---

*Introducing Devin, the first AI software engineer* is the post in which [[Organization/cognition]]
announced [[SoftwareApplication/devin]] on 12 March 2024. It presents Devin as a tireless, skilled
teammate that can either build alongside an engineer or independently complete tasks for the engineer
to review, and argues that this lets engineers focus on more interesting problems and engineering teams
aim for more ambitious goals.

The post combines a capability description, a series of demonstrations, a benchmark result and a short
statement about the company. At the time of writing Devin was in early access, with a waitlist, as
Cognition ramped up capacity.

## Key Points

- Cognition attributes Devin's ability to plan and execute complex engineering tasks requiring
  thousands of decisions to its advances in long-term reasoning and planning, and says Devin can recall
  relevant context at every step, learn over time and fix mistakes.
- Devin is equipped with common developer tools — a shell, a code editor and a browser — inside a
  sandboxed compute environment, which the post describes as everything a human would need to do the
  work.
- The post stresses collaboration as well as autonomy: Devin reports its progress in real time, accepts
  feedback, and works through design choices with the user as needed.
- Its demonstrations show Devin learning an unfamiliar technology from a blog post, building and
  deploying an interactive web app while adding features the user requests, finding and fixing bugs in
  an open-source project, setting up fine-tuning for a large language model from a link to a research
  repository, addressing a GitHub issue given only its link, and completing freelance jobs posted on
  Upwork.
- On [[Dataset/swe-bench]], which the post describes as asking agents to resolve real-world GitHub
  issues from open-source projects, Cognition reports that Devin resolved 13.86% of issues end-to-end,
  against a previous state of the art of 1.96%, and that the best previous models resolved 4.80% even
  when given the exact files to edit.
- The post qualifies that comparison itself: Devin was evaluated on a random 25% subset of the dataset,
  and was unassisted, whereas the other models were assisted — told exactly which files needed to be
  edited. Cognition says a more detailed technical report would follow.

## Context

This is a launch announcement by the vendor, and its benchmark figure is Cognition's own report of its
own evaluation on a subset of the benchmark, as the post itself states. The phrase "the first AI
software engineer" is the post's framing of its product.

The post closes with a description of Cognition as an applied AI lab focused on reasoning that is
building "AI teammates", and says code is just the beginning of what it wants those teammates to do.
