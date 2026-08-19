---
title: "AI-assisted software development"
type: "schema:DefinedTerm"
lang: en
tags: [ai-assisted-programming, terminology]
sources:
  - type: url
    url: 'https://en.wikipedia.org/wiki/AI-assisted_software_development'
    hash: sha256:f4657a94008a181fc7fcb677deb754a02e6645300e34672335697956c63b365b
  - type: url
    url: 'https://simonwillison.net/2025/Mar/19/vibe-coding/'
    hash: sha256:e725441983198e989861ffd8eb4fbccea921fa47abf24f5644429df24f706ce5
  - type: url
    url: 'https://services.google.com/fh/files/misc/2025_state_of_ai_assisted_software_development.pdf'
    hash: sha256:ebc154bec056cbe5e85fac4e00658b799f30fe548f4c46aea859cfa04f3fbd03
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The use of artificial intelligence — large language models, AI agents, and related technologies — to augment software development across the lifecycle, from code generation and completion through debugging, testing, UI design, code comprehension, and documentation."
  termCode: ""
  inDefinedTermSet: ""
---

AI-assisted software development is the use of artificial intelligence to augment software development. It draws on large language models, AI agents, and other AI technologies to assist software developers across a range of tasks in the software development life cycle — code generation, debugging, editing, testing, UI design, understanding existing code, and documentation. It is the umbrella term under which more specific practices sit: [[DefinedTerm/agentic-coding]] denotes the use of AI agents for software development, and [[DefinedTerm/vibe-coding]] denotes the subset in which the developer describes a task in a prompt and accepts generated code without thorough review.

## Usage

The umbrella covers several distinct technologies. **Source code generation** uses models trained or fine-tuned on source-code corpora to generate code from natural-language descriptions, comments, or docstrings; research on such systems commonly evaluates generated programs by functional correctness — whether the output passes automated test cases — rather than by syntax alone. **Intelligent code completion** proposes completions based on surrounding context; a 2025 literature review by Husein, Aburajouh and Catal in *Computer Standards & Interfaces* is quoted as finding that LLMs significantly enhance code completion performance across several languages and contexts. AI is also applied to **testing, debugging, code review, and analysis** — generating test cases, identifying bugs and security vulnerabilities, performing static analysis, and suggesting fixes.

Reported adoption at large technology companies is substantial. About 35% of Google's code was AI-generated in the fall of 2024, reaching 50% by the next fall, and in April 2026 it was reported that 75% of new code created within Google was AI generated and then reviewed by human engineers. In April 2025, between 20% and 30% of the code for some of Microsoft's projects was written by AI, and in April 2026 Snap said at least 65% of its new code was AI generated.

Practitioner writing draws a line inside this umbrella between using the tools responsibly and abandoning review altogether. [[Person/simon-willison]], in [[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]], argues that the job of a software developer is not just to churn out code and features but to produce code that demonstrably works, can be understood by other humans and machines, and will support continued development in future — with performance, accessibility, security, maintainability and cost efficiency all to be balanced, since on his account "software engineering is all about trade-offs". His golden rule for production-quality AI-assisted programming follows from that: he will not commit code to his repository if he could not explain exactly what it does to somebody else. Code an LLM wrote that has then been reviewed, tested and understood is, in his framing, software development rather than [[DefinedTerm/vibe-coding]], and the use of an LLM to support it is immaterial.

### Adoption, trust, and what determines the return

The largest survey evidence here is [[Report/state-of-ai-assisted-software-development-2025]], based on responses from nearly 5,000 technology professionals gathered between 13 June and 21 July 2025 together with more than 100 hours of qualitative data. Its adoption figures are near-universal — 90% of respondents use AI as part of their work and more than 80% believe it has increased their productivity — while 30% report little to no trust in AI-generated code. DORA reads that gap as maturity rather than contradiction, calling a "trust but verify" approach "a sign of mature adoption" and arguing that training should focus on teaching teams "how to critically guide, evaluate, and validate AI-generated work, rather than simply encouraging usage."

Its central claim is that the practice does not have a fixed return: "AI is an amplifier", magnifying "the strengths of high-performing organizations and the dysfunctions of struggling ones", so that the greatest returns come "not from the tools themselves, but from a strategic focus on the underlying organizational system: the quality of the internal platform, the clarity of workflows, and the alignment of teams." Without that foundation, DORA argues, AI produces "localized pockets of productivity that are often lost to downstream chaos."

The report also records a specific asymmetry in outcomes: AI adoption now improves software delivery throughput, which it describes as a shift from its previous year's findings, but continues to increase delivery instability — its reading being that "while teams are adapting for speed, their underlying systems have not yet evolved to safely manage AI-accelerated development." The conditions it identifies as amplifying the benefit are set out in the [[DefinedTerm/dora-ai-capabilities-model]], with [[DefinedTerm/platform-engineering]] and [[DefinedTerm/value-stream-management]] as its two largest supporting findings. These are associations reported from one self-reported survey, not measured effects of interventions.

## Limitations

Both ownership of and responsibility for AI-generated code are disputed. A report from the German Federal Office for Information Security is cited as finding that using AI coding assistants without careful oversight from experienced developers can introduce both minor and major security vulnerabilities, and that any productivity gain should be weighed against the cost of additional quality control and security measures. Deloitte is cited as arguing that outputs must be validated through a combination of automated testing, static analysis tools, and human review, forming a governance layer for quality and accountability.

## Related Terms

Narrower practices within this umbrella include [[DefinedTerm/agentic-coding]], [[DefinedTerm/vibe-coding]], and its disciplined counterpart [[DefinedTerm/vibe-engineering]]. The tools that carry out the work are covered under [[DefinedTerm/coding-agent]].
