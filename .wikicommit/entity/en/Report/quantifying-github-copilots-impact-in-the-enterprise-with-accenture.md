---
title: "Research: Quantifying GitHub Copilot’s impact in the enterprise with Accenture"
type: "schema:Report"
lang: en
tags: [developer-productivity, ai-coding-assistants, empirical-study]
sources:
  - type: url
    url: 'https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-in-the-enterprise-with-accenture/'
    hash: sha256:5592e6dce7f718bfb96229ef5449b2a89eb7e1f67b0667ed32f474b9556a096f
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Research GitHub conducted with developers at Accenture, published on GitHub's blog in May 2024, measuring GitHub Copilot's real-world impact in an enterprise through a randomized controlled trial, a company-wide adoption analysis and a developer survey."
  author: ["Ya Gao", "GitHub Customer Research"]
  publisher: "[[Organization/github]]"
  datePublished: "2024-05-13"
  abstract: "Reports rapid adoption of GitHub Copilot among Accenture developers, increases in pull requests, pull request merge rate and successful builds, and high developer satisfaction, and outlines how organizations can study Copilot's impact themselves."
---

A research write-up published on GitHub's blog on May 13, 2024, reporting a study GitHub ran with
Accenture to measure the impact of [[SoftwareApplication/github-copilot]] in a large, real-world
engineering organization. GitHub presents it as a step beyond its earlier lab studies of Copilot,
motivated by the introduction of its business and enterprise offerings, and describes the study as led
by GitHub Customer Research in partnership with Accenture, the Microsoft Office of the Chief Economist
and the GitHub Copilot Quality Measurement team.

The study combined three kinds of evidence. The central element was a randomized controlled trial in
which developers — working across engineering, design and testing, in roles from entry level to team
management — were randomly assigned to a group given access to Copilot or a group without it, with
DevOps telemetry collected on output performance metrics. A company-wide adoption analysis looked at
installation rates, suggestion acceptance rates and the time developers took to accept their first
suggestion, with success defined as accepting a suggestion. A survey of Copilot users at Accenture
captured how developers perceived its effect on their work. Some of the data was gathered through
public APIs from GitHub and Azure DevOps, including the GitHub Copilot Metrics API.

## Findings

- **Adoption**: 81.4% of developers installed the Copilot IDE extension on the same day they received a
  license, and 96% of those who installed it started receiving and accepting suggestions the same day;
  on average developers took one minute from seeing their first suggestion to accepting one. Over 80%
  of participants adopted Copilot successfully.
- **Usage**: 67% of respondents used Copilot at least 5 days a week, averaging 3.4 days of use per
  week, and 70% relied on it for coding tasks in a programming language they already knew. 43% found
  it "extremely easy to use" and 51% rated it "extremely useful".
- **Throughput and quality**: developers in the study saw an 8.69% increase in pull requests, a 15%
  increase in pull request merge rate and an 84% increase in successful builds. GitHub interprets the
  merge rate as a measure of quality as judged by reviewers and successful builds as quality judged by
  test automation.
- **Acceptance and retention of suggestions**: developers accepted around 30% of Copilot's suggestions
  and retained 88% of Copilot-generated characters in the editor; 90% reported committing code
  suggested by Copilot and 91% said their teams had merged pull requests containing such code.
- **Developer experience**: 90% of developers reported feeling more fulfilled in their jobs and 95%
  said they enjoyed coding more with Copilot. Fulfillment rose with usage — only "a little" for those
  using Copilot less than two days a week, "quite a bit" for more than two. 70% reported quite a bit
  less mental effort on repetitive tasks, 54% spent less time searching for information or examples,
  and a majority said they could maintain flow state while using it.

The report closes with guidance for organizations running their own studies: collect quantitative,
qualitative and operational data, prepare DevOps telemetry in line with specific goals and workflows,
and tailor success metrics to the organization's own processes. The study was conducted and published
by the vendor of the product it measures.
