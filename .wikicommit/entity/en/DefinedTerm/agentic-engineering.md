---
title: "agentic engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, ai-assisted-programming, terminology]
sources:
  - type: url
    url: 'https://zenn.dev/yamitake/articles/agentic-engineering-surpass-vibe-coding'
    hash: sha256:4c9ca54cba960a10ce98bb1494b6808a1b5a0f30f3d2049f8697244e30bca183
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A term used, and defined, in a February 2026 Japanese practitioner post for a development style in which multiple AI agents are directed and coordinated while a human retains final responsibility for architecture and quality."
  termCode: ""
  inDefinedTermSet: ""
---

Agentic engineering (エージェンティックエンジニアリング) is a term used by JJ yamitake in [[BlogPosting/agentic-engineering-surpasses-vibe-coding]], published on Zenn in February 2026, for a development style in which multiple AI agents are directed and coordinated while a human retains final responsibility for architecture and quality. The post's compact formulation is that where [[DefinedTerm/vibe-coding]] means handing everything to AI, agentic engineering means becoming the tech lead of an AI team. This is one practitioner's proposed framing rather than an established or consensus definition.

## Usage

The post positions the term as the answer to a specific 2026 situation: vibe coding having become ordinary, with non-engineers publishing dozens of web tools through it, so that the value of simply being able to write code has fallen. Its three stated limits of vibe coding — the gap between code that runs and code that is usable, generated code as an unfixable black box, and inability to handle complex requirements such as multi-system integration and legacy code — are what agentic engineering is proposed to address.

It contrasts the two across five axes: the human's role (requester versus designer and supervisor), how AI is used (one-to-one dialogue versus orchestrating multiple agents), quality control (dependent on AI versus human review and approval), scope (prototype versus production product), and required skills (prompting versus design plus prompting plus review).

Five principles are offered as its practice: decompose tasks to an appropriate granularity so each step's output can be checked; pass context explicitly through files such as `CLAUDE.md` and `README.md`; treat review as the human's job, with a checklist covering security, N+1 queries, edge cases, consistency with existing code, and test sufficiency; design for failure with feature branches, CI/CD, preview environments, and staged rollout; and keep sharpening your own expertise, on the argument that judging generated code requires knowledge that delegation will never build. The post's summary claim is that an engineer's value has moved from writing code quickly and accurately to guaranteeing the correctness of code that AI wrote.

## Related Terms

The definition overlaps substantially with [[DefinedTerm/vibe-engineering]], proposed by [[Person/simon-willison]] in October 2025 for the same disciplined end of the spectrum, and with [[DefinedTerm/agentic-software-engineering]] as framed in the academic literature — though yamitake's post references neither, and does not situate its term relative to them. Its emphasis on coordinating several agents at once connects it to [[DefinedTerm/multi-agent-orchestration]], and its explicit-context principle to [[DefinedTerm/context-files]] and [[DefinedTerm/context-engineering]]. The broader mode of working it describes is [[DefinedTerm/agentic-coding]].
