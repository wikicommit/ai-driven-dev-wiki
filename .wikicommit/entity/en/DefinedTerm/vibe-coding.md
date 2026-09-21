---
title: "Vibe Coding"
type: "schema:DefinedTerm"
lang: en
tags: [llm, ai-assisted-programming, sandboxing, terminology]
sources:
  - type: url
    url: https://simonwillison.net/2025/Mar/19/vibe-coding/
    hash: sha256:653ba52b66ad62da601ae6fd257897841726d7ac6a07029edc6d0e1c5b12188f
  - type: url
    url: https://simonwillison.net/2025/Mar/23/semantic-diffusion/
    hash: sha256:472ba908e669a42742696d92e042aca8106e1995d7e09841e4452b160c3bb490
  - type: url
    url: 'https://arxiv.org/pdf/2505.19443'
    hash: sha256:6570a1ae86ae608d97b50f389a3ae52d197c066e9bb8412ba0eaea93265f7f52
  - type: url
    url: 'https://arxiv.org/pdf/2510.12399'
    hash: sha256:e7a4dc7327555d0478beeb5067576e505fb504e405921ca26c1b0f2a12f26118
  - type: url
    url: 'https://arxiv.org/pdf/2603.11073'
    hash: sha256:b27050eee67fa3ab8d502b496b64c26c1985857ac4dabac280117ba6882031d7
  - type: url
    url: 'https://www.andrewconnell.com/articles/vibe-coding-vs-agentic-engineering/'
    hash: sha256:7e8c13f25dd70015f9995dcbf564e7a460760543e3cd12d89b9175dcdf1bf151
  - type: url
    url: 'https://simonwillison.net/2026/Feb/23/agentic-engineering-patterns/'
    hash: sha256:2e0749860bb2041b583e646cdfe9ae5c095aa1e10ca0a52b54ac9fbcf3fcb72b
  - type: url
    url: 'https://simonwillison.net/guides/agentic-engineering-patterns/what-is-agentic-engineering/'
    hash: sha256:5887de1aff52ec544bd35326f452d4de9e1c58a331298d155e4a1c9f23c87af6
  - type: url
    url: 'https://simonwillison.net/2026/May/6/vibe-coding-and-agentic-engineering/'
    hash: sha256:ad2e62c904d9fb829eaaef58183d658acec08216dd6d714f3267f5ddf6f29b9e
  - type: url
    url: 'https://jimmysong.io/zh/book/ai-handbook/sdd/overview/'
    hash: sha256:946cf421ab8284921cee80b48fc236a89feb6dfd5c4a90f01ae072227495be73
  - type: url
    url: 'https://jonghoonpark.com/2026/03/29/agentic-engineering'
    hash: sha256:92fea29c2779ce511435e3c79aeb42f9b33855c8f3a1f24849a1c6993534b024
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Building software with an LLM without reviewing the code it writes. Coined by Andrej Karpathy in early February 2025 for a deliberately unexamined, fast style of building, and argued here to be a narrow subset of AI-assisted programming rather than a synonym for it."
---

Vibe coding is the practice of building software with a large language model without reviewing the
code it produces. Andrej Karpathy, who coined the term in early February 2025, described it as
fully giving in to the vibes and forgetting that the code even exists — accepting every diff
without reading it, pasting error messages back in with no comment, and, where the model cannot
fix a bug, working around it or asking for random changes until it goes away. Writing in
[[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]], Simon Willison reduces the term to
a single operational test — whether the person building the software reviews the code — and argues
that it is already being stretched to cover every form of
[[DefinedTerm/ai-assisted-programming]], which both dilutes the term and misrepresents what
responsible AI-assisted work looks like.

## Usage

The term marks a boundary in how software is produced, not a particular tool or workflow. The same
model and editor can be used either way, and what decides the label is whether the resulting code
is read and understood before it is relied on. On Willison's account, code that an LLM wrote but
that has since been reviewed, tested, and understood well enough to explain to someone else is
ordinary software development, and the fact that an LLM produced it is immaterial.

Willison presents the narrow reading as a defence of the term rather than a criticism of it. He
argues that vibe coding lowers what is otherwise a steep initial barrier to programming, letting
people build custom tools for tedious tasks without a computer science degree or a bootcamp, and
that some of them will go on to become proficient developers. He also presents it as useful to
experienced developers as the best available way to build intuition about what LLMs can and cannot
do, reporting that he has published more than eighty experiments built this way. That figure and
that assessment are his own account of his own practice.

Within weeks of the term entering circulation the narrow reading was visibly losing ground. By late
March 2025 Willison described himself as losing the battle, saying he kept seeing the term used to
mean any time an LLM is used to write code, and named what was happening to it:
[[DefinedTerm/semantic-diffusion]], a term he had just learned for a coined word's definition
weakening as it spreads beyond the people who coined it. His diagnosis of the cause was that people
could not be trusted to read Karpathy's original post all the way to the end, where the scoping to
throwaway projects appears. Karpathy, replying to that article, wrote that it will take some time to
settle on definitions: he said he uses "vibe coding" for the occasions when he feels like the dog in
the "I have no idea what I'm doing" image, citing an iOS app he had built the night before, but that
in practice he rarely goes full out vibe coding — more often he still looks at the code, adds
complexity slowly, tries to learn over time how the pieces work, and asks clarifying questions.

By 2026 Willison was still holding the narrow reading, and had begun stating it as settled
vocabulary rather than as an argument. Introducing his guide
[[CreativeWorkSeries/agentic-engineering-patterns]] in February 2026, he glosses vibe coding by its
original definition as coding where you pay no attention to the code at all, and adds an
observation about who is doing it: the term is today often associated with non-programmers using
LLMs to write code. The guide's opening chapter restates the purpose the narrow reading serves —
that a term is needed for unreviewed, prototype-quality LLM-generated code, to distinguish it from
code the author has brought up to a production-ready standard — and repeats that extending the term
to cover any LLM-assisted code production is a mistake. It also dates the coinage against the
tooling, noting that it arrived roughly three weeks before Claude Code's original release.

What changed in 2026 was not the definition but the author's report of his own conformity to it. In
[[BlogPosting/vibe-coding-and-agentic-engineering-getting-closer]] he describes the two categories
blurring in his own work: as coding agents became more reliable he stopped reviewing every line they
write, including for production-level work, which by his own operational test moves that work toward
the side of the line he had marked as irresponsible for software other people use. His account of why
it is nonetheless defensible is an analogy to depending on another team's service — read the
documentation, use it, investigate the implementation only when it misbehaves — and he states the
analogy's limit himself: a team carries accountability and professional reputation, and a coding
agent carries neither. He names the risk in the drift as an element of the normalization of deviance,
each correct unmonitored result raising the chance of misplaced trust later.

A practitioner account from 2026 keeps the narrow reading and puts it to a different use: deciding
what to hand to an AI at all. Andrew Connell defines vibe coding as a development approach in which
you have natural-language conversations with an AI and let it build an application for you without
reviewing the generated code, and attributes the term to a February 2025 tweet by Andrej Karpathy.
His summary of the difference from [[DefinedTerm/agentic-engineering]] is about ownership: vibe
coding delegates code ownership to the AI, while agentic engineering keeps the developer's
engineering judgment in the driver's seat.

Where that account is unusual is in what it says vibe coding is *good* for. Connell holds that it
works well for low-risk tasks — his examples are collecting data on a form and processing inbound
support tickets — and for anything that does not take autonomous actions without a human in the
loop, where security is not a critical concern, and where nobody has to maintain the result over
time. He then makes a second, positive case that does not depend on risk at all: that vibe coding
is valuable precisely for people who are not engineers, letting product managers, marketers and
other stakeholders express a prototype in natural language rather than arriving with a
requirements document, and letting a team "vibe up" a prototype with a customer to reach alignment
before any production code is written.

Two further accounts use the term as the starting point of a transition rather than as a category to
defend. Both draw their own boundary at whether the work can be controlled and verified — a
criterion that overlaps the narrow reading's code-review test without being the same one.

A chapter of Jimmy Song's online handbook 智能体构建指南 treats vibe coding as a stage in a progression
of programming paradigms — tool-assisted development in the IDE era, collaborative creation in the AI
programming era, and fluid co-creation in the vibe coding era, where human and AI share one context
and one semantic space. Its argument is that the stage is unstable at team scale, and it names three
problems: context drift, where the AI forgets business boundaries; uncontrollable results, with wide
variance in code quality and security; and no standard for collaboration between human, AI and tools.
Its question is therefore whether the "vibe" can be given engineering constraints, and its answer is
[[DefinedTerm/spec-driven-development]] — turning atmosphere into structure so that collaboration
becomes controllable and verifiable. The account is unusually explicit that what changes is the whole
development paradigm and not merely the way code is written.

A Korean practitioner account reaches the same boundary from experience.
[[BlogPosting/lessons-from-releasing-a-product-with-ai-agents]] reports that working with an agent on
a real product felt closer to a fight than to vibes — its author recalls repeatedly asking the agent
why it was doing what it had been told not to — and concludes that the reality is the domain of
engineering rather than of vibes, since a tool delivers value only once its output can be controlled
and verified. That account places its own practice under [[DefinedTerm/agentic-engineering]] for that
reason, and attributes the pair of terms to Karpathy a year apart, the first in early February 2025
and the second in early February 2026.

## When It Applies

Willison sets out the conditions under which he considers vibe coding acceptable, addressed
explicitly to people new to building software:

- **Low stakes.** Weigh how much harm the code could cause if it has bugs or security
  vulnerabilities — damaged reputation, lost money, or worse — with particular care if other people
  will use it.
- **Secrets.** Anything shaped like a password or API key has to be handled deliberately, which
  means understanding how the code works rather than not reading it.
- **Data privacy.** Approach a tool with access to private data cautiously, and be sure whether
  there are paths by which that data could leave the machine.
- **Load on other services.** Code that makes requests to other platforms can raise their load and
  cost, so being a good network citizen is part of the judgment.
- **Metered spending.** Willison cites accounts of people vibe coding against an API with no
  billing limit and running up thousands of dollars in charges.

Two of these conditions cut against the practice's own premise: judging secret handling and data
egress requires understanding code that vibe coding leaves unread, so the technique is at its
safest where neither is in play. Willison's own mitigation for anything that others might use is
social rather than technical — check with someone more experienced before sharing it — and his
proposed design direction is a sandbox, as in [[SoftwareApplication/claude-artifacts]], which
constrains what unread code can reach. He notes that tools aimed initially at professional
developers, such as [[SoftwareApplication/cursor]], have far fewer such rails.

The definition given here rests on one practitioner's argued position, building on Karpathy's
coinage; the post is itself a response to the term being used more loosely elsewhere, so the narrow
reading should not be taken as settled or universal usage.

A 2025 academic review, [[ScholarlyArticle/vibe-coding-vs-agentic-coding]], illustrates the broader
usage Willison describes losing ground to: it also attributes the term's coining to Karpathy, but
defines vibe coding itself as a human-centric model in which the developer remains an active
co-creator who reviews and refines each generated piece — a description close to ordinary,
reviewed [[DefinedTerm/ai-assisted-programming]] rather than Karpathy's original "forgetting that
the code even exists." The paper contrasts vibe coding with [[DefinedTerm/agentic-coding]], where
autonomous agents plan and execute multi-step tasks with reduced human supervision.

A separate 2025 survey, [[ScholarlyArticle/a-survey-of-vibe-coding]], names the same drift explicitly
from within the broader camp: it defines vibe coding overall as validating an implementation "through
outcome observation rather than line-by-line code comprehension," but of its own five-model
taxonomy of vibe-coding practice ([[DefinedTerm/vibe-coding-development-models]]), it identifies only
one — the Unconstrained Automation Model, where AI output is trusted without review — as "the
development approach most closely aligned with the original definition of Vibe Coding." Three of its
other four named models — Iterative Conversational Collaboration, Planning-Driven, and Test-Driven —
involve some form of human review, upfront planning, or test-based verification that Karpathy's
original coinage excluded. The fifth, Context-Enhanced, is not itself a review or planning practice:
the survey describes it as an orthogonal, technical context-management capability (retrieval,
codebase indexing) that can be layered onto any of the other four models, including the
Unconstrained Automation Model itself.

Connell's conditions overlap Willison's on risk but add two of his own, both about what an AI
cannot be relied on to weigh. The first is cost: he argues these tools write working code without
optimizing for operational constraints unless told to, his example being code that fetches
Microsoft Graph data in a per-user loop rather than batching, which can exceed throttling limits
within hours of a production deployment or burn through a metered quota in a week. The second he
calls the "just because you can" problem — an AI assistant may propose a technically working
solution that the platform vendor does not support, his example being a SharePoint Framework
application customizer that rearranges the DOM on modern SharePoint pages, which he says Microsoft
explicitly does not support and which could silently void support for an entire tenant. On his
account both are the kind of judgment call a practising engineer would make and vibe coding
cannot.

The maintainability objection he raises is of the same shape. Once a solution is rolled out widely,
someone has to understand it to change or fix it, and he argues an LLM asked to analyse the
codebase later will be missing the original context from its creation that the code does not fully
reflect — adding that, at least today, a model cannot hold an application past a certain size in
its context window. His conclusion is the plainest version of the narrow reading: if you don't
understand the code, you can't debug it, extend it, or explain it to your team.

## Related Terms

- [[DefinedTerm/agentic-engineering]] — the disciplined counterpart one source contrasts it with
- [[DefinedTerm/ai-assisted-programming]] — the broader practice this term is a subset of
- [[DefinedTerm/semantic-diffusion]] — the effect this term's own reception is offered as an example of
- [[DefinedTerm/agentic-coding]] — the paradigm a 2025 academic taxonomy contrasts vibe coding with
- [[DefinedTerm/vibe-coding-development-models]] — a five-model taxonomy of practices published under this term, only one of which the source ties to the original coinage
- [[ScholarlyArticle/context-before-code]] — an experience report finding vibe coding reliable for
  scaffolding but not for architectural properties like tenant isolation and asynchronous
  processing unless explicitly prompted, proposing [[DefinedTerm/non-delegation-zone]] for the gap
- [[BlogPosting/vibe-coding-and-agentic-engineering-getting-closer]] — the same author reporting the
  boundary eroding from the disciplined side of it
- [[DefinedTerm/verification-debt]] — what accumulates when the review step the narrow definition
  turns on is skipped
