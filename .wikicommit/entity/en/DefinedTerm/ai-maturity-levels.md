---
title: "AI maturity levels"
type: "schema:DefinedTerm"
lang: en
tags: [ai-adoption, industry, autonomy-levels]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/60229/'
    hash: sha256:10d03ac2a5d00b558656acc685e174052e16d06256b8fd88f86df9be1d954d01
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/64511'
    hash: sha256:0fa964600209688a0e14a38c4200b5153352f2a460d1ad35da916bfad737e92f
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "CyberAgent's internal model of AI maturity for product-development teams, which grades how wide a scope of work AI agents take on and how the boundary of responsibility between humans and AI shifts, from code completion up to automation of the whole development process; the company's goal is to reach Level 4 by 2028."
---

AI maturity levels are an internal model defined at [[Organization/cyberagent]] for grading the AI maturity of product-development teams. As [[BlogPosting/spec-driven-development-context-engineering-custom-slash-commands]] presents it, the model describes how wide a scope of work AI agents handle and how the boundary of responsibility between humans and AI shifts, in levels running from code completion (L1) to automation of the entire development process (L4). The company's mid-term goal, as [[BlogPosting/ai-knowledge-sharing-sessions-96-products]] reports it, is for its product-development teams to reach Level 4 by 2028: a state in which the development process from requirements through deployment to production is fully automated.

## Usage

The first of those posts describes the levels as follows:

- **L1, Code-level Completion** — inline completion in the IDE, limited to syntax or a few lines of logic. The human leads and AI assists with input; no autonomous agent behaviour is involved, and the human writes all the code.
- **L2, IDE with Chat** — interactive code generation through a chat interface, producing functions, classes or unit tests. The human must supply context each time by selecting and pasting files. It needs no preparation, but output quality depends on each engineer's prompting skill and so is hard to reproduce, and the work is serial because a human keeps issuing instructions.
- **L3, Ticket to PR** — a ticket such as a GitHub issue triggers an AI agent that works up to a pull request, so implementation can proceed asynchronously and in parallel with human work. Humans still collect and attach the relevant context by hand, which the post says is costly, prone to noise or gaps, and can make writing the code oneself seem faster.
- **L4, PRD to Production** — automation of the whole development process, from specification through implementation to deployment and including the work of product managers and designers. Its defining feature is that context design and prompt engineering are systematized in advance — for example with [[DefinedTerm/custom-slash-commands]] — so that consistent, high-quality context is supplied whoever runs the process. Humans design and improve the commands, control the quality of generated specifications and artifacts, and engineer the development process; the cost is the initial investment in building the platform.

That post uses the model to argue that reaching L4 requires a shift to [[DefinedTerm/spec-driven-development]] and that the bottleneck L3 leaves — context design — is what L4 removes.

The two accounts differ on the model's extent. The second post describes the scale as having five levels, with Level 4 as the 2028 target, and says the goal was announced internally in 2025; the first lists only L1 to L4 and treats L4 as automation of the whole process,.

## Related Terms

- [[DefinedTerm/spec-driven-development]]
- [[DefinedTerm/context-engineering]]
- [[DefinedTerm/agentic-autonomy-levels]]
