---
title: "Get Shit Done"
type: "schema:SoftwareApplication"
lang: en
tags: [context-engineering, spec-driven-development, agentic-coding, framework]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.04967'
    hash: sha256:635e6e4cd572aa410a5b7b000d0057fa763bfbaca72834a18577ce02d2ea86f0
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A lightweight system of meta-prompting, context engineering and specification-driven development for use with Claude Code, operating as a layer of commands and conventions over the agent rather than as its own platform."
  applicationCategory: "DeveloperApplication"
  author: ""
  operatingSystem: ""
  softwareVersion: ""
  license: ""
---

Get Shit Done — abbreviated GSD — presents itself as a lightweight system of meta-prompting, [[DefinedTerm/context-engineering]] and [[DefinedTerm/spec-driven-development]] for use with [[SoftwareApplication/claude-code]]. Rather than defining its own platform, it operates as a layer of commands and conventions over the agent, focused on structuring the context supplied to the model and on turning broad requests into specifications and executable steps.

## Overview

In the six-dimension taxonomy of [[ScholarlyArticle/from-prompt-to-process]], GSD weighs above all in context, with only partial specification: it scores 1, 2, 0, 1, 0, 0 across specification, context, roles, execution, validation and portability — a total of 4 out of 12, the lowest of the six frameworks examined, and the only one to score zero on three separate dimensions.

## Features

Its distinguishing move is treating context assembly as an explicit engineering task: deciding what the agent should read, in what order, and under which framing before it acts. The paper places this close to the grounding concerns discussed in the specification-driven development literature.

## History

Its stated limitations are coupling and volatility. Because GSD is strongly coupled to a specific agent, its portability is more limited than that of [[SoftwareApplication/spec-kit]] or [[SoftwareApplication/openspec]], and its effectiveness depends on the quality of the prompt conventions a team adopts. The paper also notes that the repository signals a maintenance move to a new organisation, which it offers as an illustration of the volatility typical of recent community frameworks.
