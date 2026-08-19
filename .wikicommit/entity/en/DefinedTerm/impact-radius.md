---
title: "impact radius"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, code-quality]
sources:
  - type: url
    url: 'https://martinfowler.com/articles/exploring-gen-ai/13-role-of-developer-skills.html'
    hash: sha256:3e83946dbe5213c00520e761c6664ebc2bacfbf1f9f9a291ba8e521c4cdccf5c
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Birgitta Böckeler's three-way classification of AI coding missteps by how far their consequences travel — time to commit, team flow within an iteration, and long-term maintainability — where a wider radius means a longer feedback loop before anyone notices."
  termCode: ""
  inDefinedTermSet: ""
---

Impact radius is the classification [[Person/birgitta-bockeler]] uses in [[BlogPosting/the-role-of-developer-skills-in-agentic-coding]] to organise the missteps she observed while working with agentic coding assistants. It sorts them not by how wrong the AI was but by how far the consequences travel: missteps that slowed her down before commit, missteps that create friction for the team within an iteration, and missteps that damage long-term maintainability. Her governing observation is that the bigger the radius, the longer the feedback loop before a team catches the issue — which inverts the intuitive ranking, making the least visible category the most damaging.

## Usage

**Time to commit** is the innermost and, in her account, least problematic radius, because the failure is obvious and the changes will most likely never reach a commit. Her examples are code that simply does not work, where experience shows up either as fast correction or as knowing early when to give up, and misdiagnosis — an assistant that assumed a Docker build issue was due to architecture settings when the real cause was `node_modules` built for the wrong architecture.

**Team flow in the iteration** covers cases where missing review creates friction during delivery. Böckeler lists too much up-front work, where the assistant goes broad rather than implementing working vertical slices — attempting to convert all UI components at once during a stack migration rather than starting with one and integrating it with the backend; brute-force fixes instead of root cause analysis, such as raising memory settings for a Docker build rather than questioning why so much memory was needed; complicating the developer workflow, with examples including two commands to run frontend and backend instead of one and failing to ensure hot reload works; and misunderstood or incomplete requirements. She notes the open question for this radius is whether increased coding throughput exacerbates these second-order effects beyond what a team can absorb sustainably.

**Long-term maintainability** is the outermost and, she writes, most insidious radius — code that works now but will be harder to change, surfacing weeks or months later, and the category where her 20+ years of programming experience mattered most. Her examples are verbose and redundant tests, where the assistant creates new test functions rather than adding assertions to existing ones, or duplicates assertions already covered elsewhere, making the suite brittle so that one change fails many tests; lack of reuse, such as not noticing a UI component already exists and duplicating it, or using inline CSS instead of classes and variables; and overly complex or verbose code, including a refactoring that failed to recognise an existing dependency injection chain and added an unnecessary constructor parameter.

## Related Terms

The classification is a diagnostic frame for what goes wrong in [[DefinedTerm/agentic-coding]] without close supervision, and the safeguards Böckeler proposes against it — careful review, quality monitoring, shift-left checks, and team rituals — overlap with the practices [[DefinedTerm/vibe-engineering]] identifies as rewarded by LLMs. The outermost radius is closely related to the accumulation described under [[DefinedTerm/verification-debt]].
