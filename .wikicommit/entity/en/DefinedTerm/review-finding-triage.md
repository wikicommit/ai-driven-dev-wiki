---
title: "Review Finding Triage"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-code-review, code-review]
sources:
  - type: url
    url: 'https://blog.shibayu36.org/entry/2026/03/23/173000'
    hash: sha256:a771a79f6b890d1b759e457b829a20cc2db5260f647ffb876954cae0a72fb4e7
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "The step of having an AI agent critically judge whether each finding from an AI code review is actually worth acting on before fixing anything, fixing only the findings it accepts and recording a reason for each one it declines."
---

Review finding triage is a step inserted between an AI code review and the fixes that follow it: instead
of addressing every finding the reviewer raised, an agent first evaluates each finding critically —
whether it really needs to be fixed, given the project's requirements and existing code — fixes only the
ones it accepts, and records why it declined the rest. It is described in
[[BlogPosting/automating-quality-improvement-before-reviewing-ai-code]], whose author credits the idea to
an article by another developer, kawarimidoll.

## Usage

The problem it answers is that AI review output mixes useful findings with off-target and excessive ones.
The post reports that having a subagent or Codex CLI review [[SoftwareApplication/claude-code]]'s code
and then fix everything it raised sometimes left the code messier than before. With triage in place, the
same review output is filtered before any change is made.

In the post's setup the triage runs as a `/fix-review-comments` skill after three reviewer agents with
different focuses have reviewed the change in parallel. Findings that several reviewers raised on the same
spot are read as higher priority. In the example shown, ten findings came in; six were addressed (as five fixes, one of them covering a
point two reviewers shared) and four were declined with reasons that refer to the project's context — for instance that the behaviour
was intentionally specified in the requirements, or that the point was already covered by existing text.

## When It Applies

- It applies where an agent both reviews and fixes code without a human in between, so that whatever the
  review raises would otherwise be acted on automatically.
- It assumes the triaging agent has enough context — requirements, the surrounding code — to tell an
  appropriate finding from an inappropriate one; the declined items in the example are justified by
  reference to exactly that context.
- The recorded reasons for declined findings are what make the result checkable: the author presents this
  selection as the reason he can leave the fixes to run automatically, and still reads the code himself
  afterwards.
- How well established it is: the source is one developer's account of his own configuration, adapted
  from another developer's idea, with an illustrative session rather than any measurement.

## Related Terms

- [[DefinedTerm/critical-dialogue-review]] — a two-model review loop in which the implementing agent accepts, rejects or defers each finding with a recorded reason
- [[DefinedTerm/agentic-code-review]]
- [[DefinedTerm/code-review-agent]]
- [[DefinedTerm/llm-as-a-judge]]
