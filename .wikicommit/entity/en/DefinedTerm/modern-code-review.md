---
title: "Modern Code Review"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, software-quality]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2405.18216'
    hash: sha256:39ab059eaf8f98bef2576a755db6a32645ae94628f587839635c0ec0a96ff064
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Modern code review (MCR) is a lightweight, tool-assisted, collaborative process in which developers examine each other's code changes before they are integrated into the codebase, serving both quality assurance and knowledge transfer."
---

Modern code review (MCR) is a collaborative process in which developers examine each other's code changes before those changes are integrated into the codebase. [[ScholarlyArticle/a-roadmap-for-modern-code-review]] describes it as a lightweight, tool-assisted software quality assurance activity that is always implemented on top of code review tools such as GitHub, GitLab, Bitbucket, Gerrit, Crucible and Review Board, and as having evolved from informal reviews by developers sitting next to each other into more formal processes, including remote review across locations and time zones.

## Usage

The same survey gives a general workflow, while noting that it varies with each organization's process and tools: a developer creates and submits a change; one or more reviewers are assigned; reviewers comment on quality, functionality and design; the developer revises the change and replies to the comments; a reviewer approves it, or requests further revisions or escalates; and the developer merges it into the main codebase. It presents MCR as widely adopted in industrial and open-source ecosystems to ensure software quality and long-term maintainability, citing the finding that unreviewed commits are twice as likely to introduce defects as reviewed ones. Beyond finding functional bugs, security vulnerabilities and style violations, MCR is described there as a channel for knowledge transfer, expertise sharing and implicit standardization of development techniques. Against these benefits the survey sets its cost: manual inspection of complex logic is cognitively demanding, can create workflow bottlenecks that delay releases, and makes MCR an expensive, resource-intensive activity.

Research on MCR is divided in that survey into improvement techniques that automate or optimize specific review tasks — analysing code changes, recommending reviewers, synthesizing and analysing review comments, and unified automation frameworks — and understanding studies of review's quality assurance effects, process efficiency, human factors and the move toward human-AI collaboration. In that account, large language models are shifting MCR from passive tool support toward a potential human-AI partnership, alongside risks such as increased verification overhead, weakened collective accountability and the deskilling of junior developers.

## Related Terms

- [[DefinedTerm/agentic-code-review]]
- [[DefinedTerm/context-aware-code-review]]
- [[DefinedTerm/code-review-agent]]
- [[DefinedTerm/review-bottleneck]]
