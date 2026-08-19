---
title: "vibe engineering"
type: "schema:DefinedTerm"
lang: en
tags: [ai-assisted-programming, terminology, agentic-coding]
sources:
  - type: url
    url: 'https://arxiv.org/html/2510.17842v1'
    hash: sha256:787bc8812aeedac3e0166895e837e88ea57a2a23b1f901c470f6e3acf40fce47
  - type: url
    url: 'https://simonw.substack.com/p/vibe-engineering'
    hash: sha256:ef207bce62b3ace1d79b606bd1e4f06b56960f2525d3a90b75215d9f9c381aa2
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A term coined by [[Person/simon-willison]] in October 2025 for a disciplined use of AI coding agents, in which experienced engineers combine LLMs with established practices such as automated testing, planning, documentation, and code review to produce maintainable, production-quality software."
---

Vibe engineering is a term for a disciplined counterpart to [[DefinedTerm/vibe-coding]]. As described in [[ScholarlyArticle/vibe-coding-ai-native-paradigm]], it was coined by [[Person/simon-willison]] in October 2025 and encourages experienced engineers to combine LLMs with best practices such as automated testing, planning, documentation, and code review, in order to produce maintainable, production-quality software.

## Usage

The term emerged from the distinction Willison draws between vibe coding and general AI-assisted programming: on his account, a developer who carefully reviews and understands every generated line is not vibe coding at all. Vibe engineering names the deliberate, engineering-disciplined version of working with coding agents that this distinction leaves room for.

Willison's own account in [[BlogPosting/vibe-engineering]] frames the term as filling a terminology gap: with vibe coding established for the fast, loose and irresponsible end of building software with AI, there was no name for the other end, "where seasoned professionals accelerate their work with LLMs while staying proudly and confidently accountable for the software they produce." He proposes it "with my tongue only partially in my cheek," and stresses that this way of working is *difficult* — the pace at which agents churn out working code raises rather than lowers the bar for the human participant.

His central claim is that LLMs actively reward existing top-tier engineering practices. The list he gives is:

- **Automated testing** — a robust, comprehensive and stable test suite lets agentic tools "fly"; without tests an agent might claim something works without having tested it, and unrelated features can break unnoticed. He notes test-first development is particularly effective with agents that iterate in a loop.
- **Planning in advance** — iterate on a high-level plan first, then hand it to the agent.
- **Comprehensive documentation** — an LLM can only hold a subset of a codebase in context, so being able to feed it relevant documentation lets it use APIs from other areas without reading the code first.
- **Good version control habits** — being able to undo and to understand when something changed matters more when an agent made the change; he describes LLMs as "fiercely competent at Git" and better than most developers at `git bisect`.
- **Effective automation** — CI, automated formatting and linting, continuous deployment to a preview environment.
- **A culture of code review** — being fast and productive at review, rather than preferring to write code yourself.
- **A very weird form of management** — providing clear instructions, sufficient context, and actionable feedback, which he says makes existing management experience surprisingly useful.
- **Really good manual QA** — including predicting and digging into edge cases.
- **Strong research skills** — figuring out which of many approaches is best, which he says remains a blocker on unleashing an agent.
- **Shipping to a preview environment** — making review productive and reducing the risk of shipping something broken.
- **An instinct for what can be outsourced** to AI versus handled manually, which he notes keeps evolving as tools improve.
- **An updated sense of estimation** — which AI-assisted coding makes harder, not easier, since the old durations no longer hold and the new factors are still being worked out.

His summary of what this adds up to is that the engineer is now "researching approaches, deciding on high-level architecture, writing specifications, defining success criteria, designing agentic loops, planning QA, managing a growing army of weird digital interns who will absolutely cheat if you give them a chance, and spending *so much time on code review*" — and that almost all of these are already characteristics of senior engineers. The claim he draws from it is that AI tools amplify existing expertise: the more skills and experience an engineer has, the faster and better their results.

Willison also defends the name against the obvious objection. He concedes it is probably a stupid name and that "vibes" as an AI concept feels tired, but argues the term establishes a clear distinction from vibe coding and signals a harder, more sophisticated way of working. He notes he has never liked the artificial distinction between "coders" and "engineers," which he associates with gatekeeping — "but in this case a bit of gatekeeping is exactly what we need."

Bamil's paper invokes the term twice as a corrective to a specific problem it identifies with vibe coding. Under maintainability and debugging, it argues that code produced via vibe coding may not follow established architectural patterns and can be hard for others to understand, and that integrating software engineering best practices — tests, documentation, modular design — into the agentic workflow, as advocated by vibe engineering, can ameliorate this. Its conclusion suggests that vibe coding may ultimately evolve into a spectrum of practices ranging from experimental prototyping to disciplined vibe engineering.

## Related Terms

The paper characterises the ongoing debate between vibe coding and vibe engineering as underscoring the need for clear terminology and responsible practices in this area.

[[DefinedTerm/agentic-engineering]] is a separately proposed term for substantially the same disciplined end of the spectrum, arriving at an overlapping set of principles from a different author without reference to this one. The tools whose arrival Willison credits with making the practice necessary are covered under [[DefinedTerm/coding-agent]], the mode of working under [[DefinedTerm/agentic-coding]], and one structured route to the same discipline under [[DefinedTerm/spec-driven-development]].
