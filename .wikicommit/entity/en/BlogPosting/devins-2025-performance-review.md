---
title: "Devin's 2025 Performance Review: Learnings From 18 Months of Agents At Work"
type: "schema:BlogPosting"
lang: en
tags: [agents, coding-agents, legacy-modernization]
sources:
  - type: url
    url: 'https://cognition.com/blog/devin-annual-performance-review-2025'
    hash: sha256:9faf159b1a9fcb52db11ab77a27cff8fad27e55cef689d325eedb664358b64ea
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Cognition's November 2025 review of its coding agent Devin eighteen months after launch, written in the form of an employee performance review. It sorts what the vendor has seen in customer deployments into two strengths — junior-level execution at unlimited scale, and senior-level codebase understanding on demand — and three areas for improvement."
  author: "[[Organization/cognition]]"
  publisher: "[[Organization/cognition]]"
  datePublished: "2025-11-14"
---

*Devin's 2025 Performance Review* is a post by the Cognition team, published on 14 November 2025,
that assesses its autonomous coding agent [[SoftwareApplication/devin]] eighteen months after launch
by borrowing the form of an annual review for a human engineer. The post states that Devin now works
in engineering teams at thousands of companies and has merged hundreds of thousands of pull requests.

Cognition explains that it first tried to place Devin on a traditional engineering competency matrix
and found this difficult: where human engineers tend to cluster around one level, Devin is
senior-level at codebase understanding but junior at execution, and has unlimited capacity while
struggling with soft skills. The post therefore summarizes strengths and weaknesses observed in real
deployments instead, with examples and metrics that Cognition attributes to its customers. The
performance and customer metrics in it are the vendor's own report about its own product.

## Key Points

- Cognition's first strength pattern is "junior execution at infinite scale": Devin does best on
  tasks with clear, upfront requirements and verifiable outcomes that would take a junior engineer
  four to eight hours, and unlike a person it can be run in parallel without limit.
- The post places vulnerability remediation, language and framework migrations, unit-test writing
  and small tickets in that category, describing them as critical but less creative work that frees
  human engineers for higher-impact projects.
- For migrations, the post says that once Devin is given instructions on how to update each
  repository, a fleet of Devins can execute the change across every repository in parallel; the post cites a bank's proprietary ETL framework migration and a Java version upgrade
  as customer examples.
- Test generation is described as a division of labour: humans write a unit-testing playbook
  spanning a few hundred repositories, a fleet of Devins writes the tests, and code owners then
  check that all logic has been tested. Cognition reports customers' test coverage typically rising
  from 50–60% to 80–90%.
- Cognition reports that over the preceding year Devin became four times faster at problem solving
  and twice as efficient in resource consumption, and that 67% of its pull requests are now merged,
  against 34% a year earlier.
- For brownfield feature work, the post says Devin can replicate and modify code where existing code
  provides clear patterns, and that Devin pushed about a third of the commits on Cognition's own web
  app.
- The post limits Devin's role in pull-request review to a first pass that catches obvious issues,
  stating that human review is still necessary because code quality is not straightforwardly
  verifiable.
- It describes data analysis and quality assurance as unexpectedly strong uses, with users asking
  Devin questions from Slack or asking it to build dashboards.
- The second strength pattern is "senior intelligence on demand": Cognition says Devin has become
  much better at understanding large codebases — one driver, in its account, of the doubled merge
  rate — so it can document large codebases through [[SoftwareApplication/deepwiki]] and help
  engineers plan through a chat interface that explains systems with architecture diagrams, maps
  dependencies, flags breaking changes and recommends what should be done by humans versus AI.
- The first area for improvement is ambiguous requirements: the post says Devin cannot
  independently take an ambiguous coding project end-to-end using its own judgement as a senior
  engineer could, and gives visual design, where it needs specifics such as component structure,
  colour codes and spacing values, as an example.
- The second is scope change: Devin handles clear upfront scoping well but usually performs worse
  when told more after starting a task, which the post contrasts with a human junior who can be
  coached through iterative problem solving. It concludes that engineers carry more responsibility
  for scoping work up front and have to learn to "manage" Devin.
- The third is soft skills: Devin collaborates in Slack, Teams and Jira but cannot manage reports or
  stakeholders or deal with teammates' emotions.

## Context

The post is a vendor's account of its own product and closes by inviting readers to talk to
Cognition's sales team; its customer outcomes are reported by Cognition rather than by the customers
themselves. Its stated weaknesses and strengths rest on the same condition: clear, verifiable
requirements are where the post says Devin succeeds, and ambiguous or shifting requirements are
where it says Devin falls short.

For 2026, Cognition states it will continue to work on making Devin better at understanding
real-world codebases and on using that context to collaborate with engineers on end-to-end software
engineering work, and is investing in the user experience so that Devin is easier to direct in
everyday development.
