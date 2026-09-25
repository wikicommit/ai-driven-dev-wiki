---
title: "SWE-bench Multimodal"
type: "schema:Dataset"
lang: en
tags: [benchmarks, evaluation, coding-agents, multimodal]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2410.03859'
    hash: sha256:964b7d943c0765ada1470231e72a7d8173927be5bc04def7158213ddca7a6fa5
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A benchmark of real-world bug-fixing tasks from user-facing JavaScript libraries, each with at least one image or video in its problem statement or tests, built on the SWE-bench task formulation to evaluate systems on visual software domains."
---

SWE-bench Multimodal (SWE-bench M) is a benchmark of software engineering tasks drawn from GitHub
issues in user-facing JavaScript repositories — libraries for web interface design, diagramming,
data visualization, syntax highlighting and interactive mapping — in which every task contains
visual content. It was built by the authors of
[[ScholarlyArticle/swe-bench-multimodal-do-ai-systems-generalize-to-visual-software-domains]] to
evaluate whether systems developed for the Python-only [[Dataset/swe-bench]] generalize to other
programming languages and to problems that have to be understood visually.

## Contents

Each task instance follows the SWE-bench formulation: a codebase and an issue (the problem
statement), a reference solution from the corresponding pull request, and unit tests — fail-to-pass
tests that the fix must make pass and pass-to-pass tests that check existing behavior is kept. The
paper reports 619 task instances from 17 repositories, divided into a test split of 517 instances
from 12 repositories and a development split of 102 instances from 5 repositories chosen to mirror
test repositories with a similar purpose. Repositories include bpmn-js, carbon, Chart.js,
highlight.js, lighthouse, openlayers, p5.js and prettier, and every selected repository is at least
70% JavaScript or TypeScript.

The problem statements carry 862 images, which annotators grouped into categories led by website
screenshots and code screenshots, followed by diagrams, error messages, art, maps and data
visualizations; many tasks have several images or a video. A subset of 69 tasks checks
correctness with pixel-level visual testing, comparing rendered screenshots. The paper reports 55 tasks whose
problem statement text or images use languages other than English, with Mandarin Chinese among
them in 38 tasks.

## Provenance

The authors searched GitHub for JavaScript repositories with at least 5,000 stars and 500 pull
requests, manually picked 17 user-facing libraries, and scraped their pull requests. They kept
issue and pull-request pairs whose issue text or test patch links to an image or video, added
Node.js and Chrome support to SWE-bench's Docker setup and wrote per-repository installation and
test scripts, removed tests whose results were inconsistent across repeated runs, and had the
authors manually inspect every remaining instance, removing 24 judged impossible. Images, videos
and reproduction code linked from issues, including code from online editors such as CodeSandbox
and JSFiddle, were downloaded so the problem statements remain reproducible if the links expire.
The paper lists the license of each repository and states that data, code and a leaderboard are
available at swebench.com/multimodal.

## Use

In the introducing paper, RAG, [[SoftwareApplication/swe-agent]] in three configurations and an
adapted Agentless were evaluated on the benchmark; the SWE-agent configurations resolved the most
tasks, and the authors attribute Agentless's weak results on it to a localization module designed
around Python.
