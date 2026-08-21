---
title: "google/skills"
type: "schema:SoftwareApplication"
lang: en
tags: [agent-skills, google-cloud, agentic-coding, open-source]
sources:
  - type: url
    url: 'https://github.com/google/skills'
    hash: sha256:2cd546f966e823a193b2fe7ded97411a80bdb5450a80bc311f1b4a2f5495e4d8
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Google's official repository of Agent Skills for its products and technologies, organised by domain and installable across agent harnesses, which also bundles product plugins pairing skills with MCP servers."
  applicationCategory: "DeveloperApplication"
  author: "[[Organization/google]]"
  operatingSystem: ""
  softwareVersion: ""
  license: "Apache-2.0"
---

`google/skills` is Google's official repository of [[DefinedTerm/agent-skills]] for its products and technologies, including Google Cloud. Its README carries a note that the repository is under active development. Installation is a single command, `npx skills add google/skills`, from which specific skills can be selected rather than installing everything.

## Overview

The skills are grouped by domain rather than by product line. Getting-started material covers authenticating to Google Cloud, a foundation-builder recipe, and onboarding. Multi-product **solution** skills cover whole architectures — a solution-architecture workflow, agentic analytics across cloud providers and data types, an open data lakehouse system, building and deploying agents on Google Cloud, a data-science workflow, bidirectional multimodal streaming, migrating AI workloads to GKE inference, RAG for enterprise search on GKE and AlloyDB, and a secure n-tier serverless web application. Further groups cover AI/ML (including a set of Agent Platform skills for inference, deployment, tuning, prompt management, RAG engine management, model registry, alerting and troubleshooting, plus Gemini API skills), infrastructure (largely GKE), observability and cost, the six Well-Architected Framework pillars, security and identity, web and app hosting, advertising, and analytics.

## Features

Beyond skills, the repository bundles Google product **plugins** that pair skills with MCP servers for agent harnesses, with documented install paths for three: [[SoftwareApplication/claude-code]] (`claude plugin marketplace add google/skills`, then `claude plugin install <plugin>@google-plugins`), [[SoftwareApplication/codex]] (`codex plugin marketplace add google/skills`, then installing from the plugins browser), and Antigravity CLI (`agy plugin install` with a plugin path).

The README also points to further Google skill collections maintained in separate repositories, covering Cloud Storage, the Agent Development Kit, Android, Dart, Firestore, Flutter and Genkit.

## History

The repository was announced at Google Cloud Next 2026 in [[BlogPosting/level-up-your-agents-google-skills-repository]], which described a launch set of thirteen skills and promised more in the following weeks and months; the catalogue described above is the considerably larger set present at the time of this snapshot. At that snapshot the repository shows 18.6k stars, 1.5k forks and 265 commits, carries an Apache 2.0 licence, and invites contributions in the form of bug reports against the skill Markdown files and feature requests proposing new skills.
