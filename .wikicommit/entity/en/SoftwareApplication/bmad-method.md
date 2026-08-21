---
title: "BMAD Method"
type: "schema:SoftwareApplication"
lang: en
tags: [spec-driven-development, multi-agent, agentic-coding, framework]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An open framework for agile development with AI, organised as an ecosystem of modules, workflows, skills and artifacts, with specialised agents standing in for classic software development roles across a phased flow."
  applicationCategory: "DeveloperApplication"
  author: ""
  operatingSystem: ""
  softwareVersion: ""
  license: ""
---

The BMAD Method is an open framework aimed at agile development with AI. Its unit of organisation is not the individual agent but an ecosystem of modules, workflows, skills and artifacts. Its documentation, as reported in [[ScholarlyArticle/from-prompt-to-process]], describes a phased flow with optional analysis, planning, solution and implementation phases plus a quick flow for smaller tasks, and presents the framework as an approach to AI-native development installed via `npx bmad-method install`.

## Overview

In the six-dimension taxonomy that paper proposes, BMAD stands out in roles, specification and context, scoring 2, 2, 2, 1, 2, 1 across specification, context, roles, execution, validation and portability — a total of 10 out of 12, the highest of the six frameworks examined. Its stated weakness is the mirror image: the deepest process in the set comes at the cost of portability and execution.

## Features

Its default agents represent classic software development functions — analyst, product manager, architect, developer, UX designer and technical writer. Each role triggers workflows that produce documents or decisions consumed by the next phase, so that architecture informs stories, stories inform implementation, and reviews and readiness checks act as gates. The paper's stated reason this progression matters is that it prevents the implementation agent from operating on a short instruction alone. Its artifact progression runs product brief, PRD, architecture, epics, stories and code review.

## History

The paper's assessment is that BMAD's strength is turning human-AI collaboration into a process recognisable by software teams: rather than replacing agile practices, it tries to make PRDs, architecture, epics, stories and reviews consumable by agents. Its stated fragility, from a research standpoint, is that effectiveness depends on usage discipline and on independent empirical evaluation that has not yet been done — the framework supplies structure, but when that structure improves quality, time, cost, maintenance and alignment remains unmeasured. The comparison table records its dominant risk as "process cost and need for usage discipline."
