---
title: "agentic engineering"
type: "schema:DefinedTerm"
lang: en
tags: [agentic-coding, ai-assisted-programming, terminology]
sources:
  - type: url
    url: 'https://zenn.dev/yamitake/articles/agentic-engineering-surpass-vibe-coding'
    hash: sha256:4c9ca54cba960a10ce98bb1494b6808a1b5a0f30f3d2049f8697244e30bca183
  - type: url
    url: 'https://blog.matthewbrunelle.com/agentic-engineering-is-just-everything-we-havent-been-doing/'
    hash: sha256:a57c3f89f2c2b54dd0f3a7abd19439524919c3c76a1c07c94e04bb4f203ce639
  - type: url
    url: 'https://nyosegawa.com/en/posts/coding-agent-workflow-2026/'
    hash: sha256:bb7d36388cc5d0dc91fc90185585f6fff68833b1b198e732c6e2d6d41a285f45
  - type: url
    url: 'https://simonwillison.net/guides/agentic-engineering-patterns/what-is-agentic-engineering/'
    hash: sha256:e6c2c65056d73b991e32cf28fde817d0bb3d43f3a9824b25ae882a93a180b6a6
  - type: url
    url: 'https://simonwillison.net/2026/May/6/vibe-coding-and-agentic-engineering/'
    hash: sha256:d5efc58fb9f6c8e44c88eb246031dace67556db67152702ac3bb82b8c358bb3a
review_status: pending
generated_at: "2026-08-21"
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

### The deflationary reading

Not every account treats the term as naming something new. [[BlogPosting/agentic-engineering-is-just-everything-we-havent-been-doing]] argues that the practices people get excited about when improving agentic engineering are the ordinary software engineering practices teams already should have had — "the kind of work we typically cut because of time pressure" — and lists them plainly: docstrings, descriptive pull requests, current documentation, meaningful tests, agreed code conventions and automated linting, design feedback before implementing, recorded meeting decisions, and conversations held in open searchable channels rather than DMs. Its compact form of the claim is that "agentic engineering is just normal engineering with robots."

The post's contribution beyond the deflation is its corollary: **anything that makes engineering harder makes agentic engineering much harder**, because an agent lacks the situational judgement — it borrows James C. Scott's term *mētis* — that lets a person navigate a broken situation. Its practical advice follows from that: if agentic engineering is going badly, check whether ordinary engineering is also hard at that company, because "slapping AI on a dysfunctional system, be it people or software, will not fix your problems."

It also records one way the new context genuinely changes the calculus rather than merely re-motivating old practice. A coworker is quoted observing that encoding guiding principles into documentation now has an effect it previously would not have had: before, making principles stick would have required a team conversation and memorisation, whereas now every engineer's agent reads the documentation and adheres to it. The author's own limit on this is that free-form engineering principles resist being made legible in a way code syntax does not — "a written rule is not a judgment" — while conceding that a frozen legible system beats nothing at all.

### A different origin story for the same term

[[BlogPosting/survey-of-development-workflows-in-the-coding-agent-era]] gives the term a lineage that the practitioner framings above do not. It reports that Karpathy proposed vibe coding in February 2025, that over the following year it matured from "let a coding agent write code on vibes" into a structured engineering methodology, and that in February 2026 Karpathy *renamed* it agentic engineering — with the definition that you do not write code directly and 99% of your time goes to orchestrating and supervising the agents that do. That survey attributes the renaming account to a trade-press piece rather than reporting it firsthand.

It also relays two other systematisations. From Addy Osmani: that successful developers spend 70% of their time on problem definition and verification strategy and 30% on execution — the reverse of the traditional split — while total time falls dramatically; and a mindset shift from crafting software by hand one piece at a time to operating an automated assembly line. From [[Person/simon-willison]]: a set of codified practical patterns the survey lists as Red/Green TDD, Writing Code is Cheap Now, First Run the Tests, Linear Walkthroughs, and Hoard Things You Know How to Do.

The survey's own contribution is structural rather than definitional: it treats agentic engineering as something you design across three layers — project workflows, in-session implementation techniques, and infrastructure — with harness engineering as the implementation foundation underneath.

### The definition Willison uses

[[TechArticle/what-is-agentic-engineering]] gives the term the narrowest of the definitions collected here — the one its author says he uses: "the practice of developing software with the assistance of coding agents." Everything else in that chapter follows from unpacking the pieces — a [[DefinedTerm/coding-agent]] is an agent that can both write and execute code, and an agent is software that "run[s] tools in a loop to achieve a goal."

Two claims in that chapter give the term its content beyond the definition. The first is that code execution is the defining capability: without the ability to run the code, anything an LLM outputs is of limited value, and with it agents can iterate toward software that demonstrably works. The second answers what remains for the human — writing code was never the sole activity of a software engineer, and the craft has always been figuring out *what* code to write, navigating dozens of possible solutions to fit a particular set of circumstances. In practice that means supplying the agent with the right tools, specifying the problem at the right level of detail, and verifying and iterating until the result is robust and credible.

That chapter also relocates learning from the model to the harness: LLMs do not learn from their past mistakes, but coding agents can, provided the human deliberately updates instructions and tool harnesses to reflect what was learned. Its stated ambition for the practice is not merely speed — "coding agents can help us be much more ambitious with the projects we take on," producing more, better-quality code against more impactful problems.

### The boundary eroding in its own author's practice

[[BlogPosting/vibe-coding-and-agentic-engineering-are-getting-closer]] records [[Person/simon-willison]] observing that the distinction he drew has blurred in his own work. His stated version of agentic engineering there is a professional standard rather than a technique: you are a professional software engineer who understands security, maintainability, operations and performance, using the tools to the highest of your own ability, still leaning on decades of experience — with the goal being higher-quality software faster, since "if you're building lower quality stuff faster, I think that's bad."

The erosion he reports is at the review step. As agents became more reliable he stopped reviewing every line even for production work, which by his own earlier definition moves the practice toward [[DefinedTerm/vibe-coding]]. His reconciliation is to treat an agent's output like another team's internal service — read the documentation, use it, and only open the repository when something looks wrong — while naming exactly why the analogy is imperfect: a human team carries a professional reputation and accountability, and an agent does not. He names the risk as the normalization of deviance, where each unmonitored success raises the chance of misplaced trust later.

## Related Terms

The definition overlaps substantially with [[DefinedTerm/vibe-engineering]], proposed by [[Person/simon-willison]] in October 2025 for the same disciplined end of the spectrum, and with [[DefinedTerm/agentic-software-engineering]] as framed in the academic literature — though yamitake's post references neither, and does not situate its term relative to them. Its emphasis on coordinating several agents at once connects it to [[DefinedTerm/multi-agent-orchestration]], and its explicit-context principle to [[DefinedTerm/context-files]] and [[DefinedTerm/context-engineering]]. The broader mode of working it describes is [[DefinedTerm/agentic-coding]].
