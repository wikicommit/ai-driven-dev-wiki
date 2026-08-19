---
title: "The role of developer skills in agentic coding"
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, code-quality, ai-assisted-programming]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/13-role-of-developer-skills.html'
    hash: sha256:3e83946dbe5213c00520e761c6664ebc2bacfbf1f9f9a291ba8e521c4cdccf5c
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A 25 March 2025 memo by Birgitta Böckeler cataloguing concrete cases where she had to steer agentic coding assistants, organised by [[DefinedTerm/impact-radius]] — from wasted time before commit through to long-term maintainability damage."
  author:
    - "[[Person/birgitta-bockeler]]"
  datePublished: "2025-03-25"
  publisher: "martinfowler.com"
---

"The role of developer skills in agentic coding" is a 25 March 2025 memo by [[Person/birgitta-bockeler]], published on martinfowler.com as part of the "Exploring Gen AI" series. It responds to two opposing reactions to agentic coding assistants — that developers will be unnecessary within a year, and that the quality of AI-generated code and the challenge of preparing junior developers are causes for concern — by listing concrete cases from the author's own use of agentic modes in Cursor, Windsurf, and Cline, almost exclusively on existing codebases rather than greenfield projects.

The memo is positive about the tools' progress: it credits IDE integration with letting assistants run tests and other development tasks and try to immediately fix the errors that occur, automatically pick up on and try to fix linting and compile errors, do web research, and in some cases read browser console errors or inspect DOM elements. Böckeler reports impressive collaboration sessions and features built in record time.

Its central "however" is that even in those successful sessions she intervened, corrected, and steered constantly, and often decided not to commit the changes at all. The stated purpose of listing the interventions is to illustrate which developer skills remain necessary in "supervised agent" mode — the skills, in her framing, that we have to preserve and train for.

## Key Points

- **Three impact radiuses.** Böckeler categorises AI missteps by how far their consequences travel: slowing down time to commit, creating friction for team flow within an iteration, and damaging long-term maintainability. She notes the bigger the radius, the longer the feedback loop before a team catches the problem. See [[DefinedTerm/impact-radius]].
- **Time to commit.** The least problematic category, because the failure is obvious and the changes usually never reach a commit. Examples: code that simply does not work, and misdiagnosis — the assistant blamed a Docker build's architecture settings when the real cause was `node_modules` built for the wrong architecture.
- **Team flow.** Going broad instead of implementing working vertical slices (converting all UI components at once during a stack migration); brute-force fixes instead of root cause analysis (raising memory settings rather than asking why a Docker build needed that much memory); build workflows that degrade the developer experience for everyone; and jumping to conclusions when requirements were not described in detail.
- **Long-term maintainability.** The most insidious radius, and the one where Böckeler says her 20+ years of programming experience mattered most: verbose and redundant tests that make the suite brittle, code that lacks modularity and duplicates work already implemented elsewhere, and overly complex or verbose code — including a refactoring in which the assistant failed to recognise an existing dependency injection chain and added an unnecessary constructor parameter.
- **Prompting mitigates but does not control.** She prefaces the list by noting that custom rules and additional prompting can mitigate many of these, but that LLMs frequently do not follow the letter of the prompt, and that the longer a session gets the more hit-and-miss adherence becomes.
- **A calibrated forecast.** Böckeler writes that by no stretch of her imagination will AI write 90% of code autonomously within a year, but allows it may *assist* in writing 90% for some teams and codebases; she reports it assisting her in 80% of cases in a moderately complex 15K-LOC codebase.

## Context

The memo closes with safeguards rather than conclusions. For individual coders: always review AI-generated code carefully; stop a session when overwhelmed and either revise the prompt or fall back to manual implementation — "artisanal coding," a phrase she credits to her colleague Steve Upton; stay cautious of "good enough" solutions produced very quickly; and practice pair programming. For teams and organisations: code quality monitoring with tools such as Sonarqube or Codescene, watching duplication in particular; pre-commit hooks and IDE-integrated review to shift checks left; rituals such as a weekly-reviewed "Go-wrong" log; team-level custom rule sets, with the same caveat that adherence is not guaranteed; and a culture of trust, on the argument that organisations pressuring teams to deliver faster "because you now have AI" are more exposed to the quality risks described.

The account is explicitly one practitioner's, drawn from a small codebase and a specific set of tools at a specific point in 2025, and Böckeler frames the examples as having a non-negligible probability of recurring rather than as things the tools always do.
