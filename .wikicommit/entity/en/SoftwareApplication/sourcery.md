---
title: "Sourcery"
type: "schema:SoftwareApplication"
lang: en
tags: [code-review, coding-tools, llm]
sources:
  - type: url
    url: 'https://aise.phodal.com/aise-code-review.html'
    hash: sha256:c66c9a026df66e7f4feae11ee51fd39f0d6479793176e5269c0d01403e7f9453
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An AI code review tool whose published engineering approach splits a pull request's diff into small chunks, filters out unpromising ones deterministically before calling an LLM, and runs a second LLM pass to discard overly generic review comments."
  applicationCategory: "AI code review tool"
---

Sourcery is an AI code review tool. Phodal's book on AI-assisted software engineering uses it, in its chapter on code review, as a worked example of how an LLM-based reviewer is engineered, summarising several of Sourcery's own published write-ups: how it checks a change for unnecessary complexity, how it prompts, how it tests LLM output, and how it improves the usefulness of the comments it generates.

## Capabilities

Its approach to complexity in review targets accidental complexity — complexity introduced into code that the task does not require — rather than the essential complexity of a hard problem. The Sourcery write-up the chapter draws on names four signs a reviewer should look for: code that rebuilds existing functionality or duplicates code, a lack of decoupling where one unit tries to do too much, deep nesting or high cognitive or cyclomatic complexity, and over-engineering, such as needlessly anticipating future features or edge cases that may never occur.

The review pipeline is built around the view that simply giving an LLM more context has diminishing returns, can hurt accuracy by producing false positives or hallucinations, and is expensive. It therefore proceeds in steps: split the diff into atomic chunks of related changes, such as changes within the same function or class; drop chunks that heuristic checks show cannot affect complexity, such as a new import or a very small change, without involving the LLM; expand each remaining chunk with the surrounding lines it needs; have the LLM turn its reasoning into a comment useful to the developer; and finally send each comment to another LLM request that discards it if it is too generic. The chapter reports that this final filter removed most false positives in Sourcery's experiments, and that in the worked example it describes, the multi-step design used far fewer tokens than a single request with expanded context.

The chapter's Sourcery example also illustrates the [[DefinedTerm/panel-of-experts-prompting]] technique, with prompts for deciding which docstrings a diff requires updating. Sourcery's LLM outputs are unit-tested with pytest, much like ordinary unit tests: rather than checking the exact wording of a comment, the tests check that the type the LLM assigned it from a fixed set matches the type expected for that diff, look for expected keywords or themes, confirm that irrelevant feedback such as praise is absent, and check that a comment is attached to the right line. Because LLM output varies, its CI tolerates some failures, requiring 95% of LLM tests to pass.

To improve generated review comments it treats usefulness to the pull request's author as more important than accuracy, measured as the share of generated comments judged useful. Adjusting prompts or asking the LLM to explain a comment's usefulness had limited effect, since the model tends to be confident its own output is useful; what worked was validating each comment against several criteria — relevance to the code, actionability, specificity and value to the author — and combining them to filter comments.

## Adoption & Ecosystem

Besides its own worked-example section, Sourcery appears in the chapter's list of other AI code review tools, alongside products such as [[SoftwareApplication/greptile]], Codeant AI, Bito and Sweep AI. The chapter covers [[SoftwareApplication/coderabbit]] and [[SoftwareApplication/pr-agent]] in sections of their own.
