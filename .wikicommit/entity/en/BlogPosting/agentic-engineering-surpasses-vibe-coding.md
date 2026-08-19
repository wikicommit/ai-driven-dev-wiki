---
title: "バイブコーディングはもう古い！エージェンティックエンジニアリングで差をつけろ"
type: "schema:BlogPosting"
lang: en
tags: [agentic-coding, ai-assisted-programming, code-quality]
sources:
  - type: url
    url: 'https://zenn.dev/yamitake/articles/agentic-engineering-surpass-vibe-coding'
    hash: sha256:4c9ca54cba960a10ce98bb1494b6808a1b5a0f30f3d2049f8697244e30bca183
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A 24 February 2026 Japanese-language Zenn post arguing that vibe coding has become table stakes and that professional engineers should move to [[DefinedTerm/agentic-engineering]], set out as a definition, a comparison table, and five principles."
  author:
    - "JJ yamitake"
  datePublished: "2026-02-24"
  publisher: "Zenn"
---

"バイブコーディングはもう古い！エージェンティックエンジニアリングで差をつけろ" ("Vibe coding is old news — get ahead with agentic engineering") is a Japanese-language post published on Zenn on 24 February 2026 by JJ yamitake, a Rails engineer and representative of Yapr LLC. Its premise is that by 2026 [[DefinedTerm/vibe-coding]] has become ordinary — the author points to non-engineers publishing dozens of web tools through services built around it — and that the value of simply being able to write code is falling fast.

The post's answer for professional engineers is [[DefinedTerm/agentic-engineering]], which it defines as a development style in which multiple AI agents are directed and coordinated while a human retains final responsibility for architecture and quality. Its slogan for the shift is that where vibe coding means handing everything to AI, agentic engineering means becoming the tech lead of an AI team.

This is one practitioner's opinion piece, not a survey or a study; the five principles it offers are presented as practical advice rather than as validated findings.

## Key Points

- **Three stated limits of vibe coding.** That there is a gap between code that runs and code that is usable — missing error handling, security holes such as SQL injection and XSS, performance problems such as N+1 queries and memory leaks, and unmaintainable code; that generated code is a black box which nobody can fix once problems surface, compounding technical debt until rewriting is faster; and that it cannot handle complex requirements such as multi-system integration, legacy code, bespoke business logic, and scalability.
- **A comparison table.** The post contrasts the two along five axes: the human's role (requester vs. designer and supervisor), how AI is used (one-to-one dialogue vs. orchestrating multiple agents), quality control (dependent on AI vs. human review and approval), scope (prototype vs. production product), and required skills (prompting vs. design plus prompting plus review).
- **Five principles.** Decompose tasks to an appropriate granularity, so each step's output can be checked and corrected; pass context explicitly, using files such as `CLAUDE.md` and `README.md` to structure project background, constraints, and coding conventions; treat review as the human's job, with a checklist covering security holes, N+1 queries, edge cases, consistency with existing code, and test sufficiency; design for failure, using feature branches, CI/CD, preview environments, and staged rollout; and keep sharpening your own expertise, on the argument that judging generated code requires domain, architecture, security, and performance knowledge that delegation will never build.
- **A shift in what engineers are for.** The post's closing claim is that an engineer's value has moved from writing code quickly and accurately to guaranteeing the correctness of code that AI wrote, and it frames this as evolution rather than decline — comparing it to surgeons using robots and pilots using autopilot, while noting that using a tool well requires more knowledge than the tool itself has.

## Context

The post names Claude Code as, in its author's assessment, the most practical environment for this way of working as of February 2026, and includes an ASCII diagram of a human tech lead directing implementation, testing, and refactoring agents.

Its terminology sits alongside rather than inside the existing vocabulary: the definition it gives for agentic engineering overlaps substantially with [[DefinedTerm/vibe-engineering]], proposed for the same disciplined end of the spectrum, and with [[DefinedTerm/agentic-software-engineering]] as framed in the academic literature — but the post does not reference either, and does not position its term relative to them.
