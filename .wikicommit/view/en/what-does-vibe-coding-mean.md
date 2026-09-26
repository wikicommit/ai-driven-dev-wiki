---
title: "What does \"vibe coding\" mean?"
lang: en
kind: debate
review_status: pending
generated_at: "2026-09-26"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
derived_from:
  - path: .wikicommit/entity/en/DefinedTerm/vibe-coding.md
    source_commit: 20326ae2b2d3074fa7e5e75e7d6a666eb50f9daf
  - path: .wikicommit/entity/en/BlogPosting/not-all-ai-assisted-programming-is-vibe-coding.md
    source_commit: a2a36121909aa23634f929ee05bc57eb32194828
  - path: .wikicommit/entity/en/BlogPosting/two-publishers-and-three-authors-fail-to-understand-what-vibe-coding-means.md
    source_commit: 8747b8ec3dcc7491d2de6b080020106d3f5da014
  - path: .wikicommit/entity/en/BlogPosting/vibe-coding-and-agentic-engineering-getting-closer.md
    source_commit: a2a36121909aa23634f929ee05bc57eb32194828
  - path: .wikicommit/entity/en/DefinedTerm/semantic-diffusion.md
    source_commit: a2a36121909aa23634f929ee05bc57eb32194828
  - path: .wikicommit/entity/en/ScholarlyArticle/a-survey-of-vibe-coding.md
    source_commit: a2a36121909aa23634f929ee05bc57eb32194828
  - path: .wikicommit/entity/en/ScholarlyArticle/building-software-by-rolling-the-dice.md
    source_commit: a2a36121909aa23634f929ee05bc57eb32194828
  - path: .wikicommit/entity/en/Book/beyond-vibe-coding.md
    source_commit: 8747b8ec3dcc7491d2de6b080020106d3f5da014
  - path: .wikicommit/entity/en/Book/vibe-coding-building-production-grade-software.md
    source_commit: 8747b8ec3dcc7491d2de6b080020106d3f5da014
  - path: .wikicommit/entity/en/DefinedTerm/agentic-engineering.md
    source_commit: a2a36121909aa23634f929ee05bc57eb32194828
---

Andrej Karpathy coined "vibe coding" in early February 2025, and within weeks the narrow reading of it
was already losing ground. The pages collected here answer the question "what does the term name?"
in different ways. Some hold it to the
coinage: building software with an LLM without reviewing the code it produces. Others use it as an
umbrella for almost any prompt-driven development, reviewed or not. A third group draws the line
somewhere else entirely. This page lays those answers side by side, along with what each one rests
on. It does not pick one.

## The narrow answer: code nobody reviewed

The most sustained case for the narrow reading comes from Simon Willison. In
[[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]] he reduces the term to one observable
test: whether the person building the software reviews the code the LLM writes. By that test, code
an LLM wrote that has since been reviewed, tested, and understood well enough to explain to someone
else is ordinary software development, and the LLM's part in it is immaterial. Treating vibe coding
as a synonym for [[DefinedTerm/ai-assisted-programming]], he argues, gives a false impression of
what responsible AI-assisted programming can achieve.

His evidence is the wording of the coinage itself. He quotes Karpathy's original description in full
to show that it already limited the practice to throwaway weekend projects and spoke of forgetting
that the code even exists. In
[[BlogPosting/two-publishers-and-three-authors-fail-to-understand-what-vibe-coding-means]] he calls
the distinction "a hill I am willing to die on". By February 2026 he was presenting the narrow
reading as settled vocabulary rather than as an argument. He explained its purpose as having a term
for unreviewed, prototype-quality LLM-generated code, distinct from code brought up to a
production-ready standard.

Narrowing the term is not the same as condemning the practice. Willison argues that vibe coding
lowers a steep barrier to programming, and that it is the best available way for experienced
developers to build intuition about what LLMs can do. He also sets out the conditions under which
he considers it acceptable: low stakes, care with secrets and private data, the load it puts on
other services, and metered spending.

Andrew Connell's account, recorded on [[DefinedTerm/vibe-coding]], keeps the same boundary and
recasts it as a question of ownership. Vibe coding hands ownership of the code to the AI;
[[DefinedTerm/agentic-engineering]] keeps the developer's engineering judgment in the driver's seat.

## The umbrella answer: building mainly by prompting

A second group of pages uses the term far more broadly, and several of them acknowledge that they
are doing so.

[[ScholarlyArticle/a-survey-of-vibe-coding]] defines vibe coding as validating an implementation
"through outcome observation rather than line-by-line code comprehension". Inside that definition it
proposes a five-model taxonomy ([[DefinedTerm/vibe-coding-development-models]]). Of the five, it
names only the Unconstrained Automation Model, where AI output is trusted without review, as "the
development approach most closely aligned with the original definition of Vibe Coding". Three of the
others involve human review, upfront planning, or test-based verification, all of which the original
coinage left out. The survey therefore uses the umbrella sense while pointing to where the narrow
sense sits inside it.

A 2025 academic review, [[ScholarlyArticle/vibe-coding-vs-agentic-coding]], goes further, as reported
on [[DefinedTerm/vibe-coding]]. It defines vibe coding as a human-centric model in which the developer
reviews and refines each generated piece, which is close to ordinary reviewed AI-assisted
programming. It contrasts that with [[DefinedTerm/agentic-coding]].

[[ScholarlyArticle/building-software-by-rolling-the-dice]] studies the term's actual use rather than
proposing a definition. It describes vibe coding as an umbrella covering everything from fully
delegating to autonomous agents to agent-supported engineering that still involves manual editing and
inspection. The practitioners it observed disagreed with one another: some argued for a strict
definition, while others rejected any boundary between vibe coding and traditional software
engineering. The authors present their findings as a snapshot, not as a ruling on what should count.

The umbrella sense also reached book titles. [[Book/vibe-coding-building-production-grade-software]]
by Gene Kim and Steve Yegge is subtitled "Building Production-Grade Software With GenAI, Chat,
Agents, and Beyond". Addy Osmani's O'Reilly book was first announced as "Vibe Coding: The Future of
Programming". Willison argued that both describe exactly what vibe coding is not. Osmani's book was
later retitled [[Book/beyond-vibe-coding]], a change Willison welcomed.

## A third answer: draw the line at control, not at review

Several accounts on [[DefinedTerm/vibe-coding]] use a boundary that overlaps with the review test
without being the same thing.

- A chapter of Jimmy Song's handbook treats vibe coding as a stage in a progression of programming
  paradigms. It argues that the stage is unstable at team scale and answers with
  [[DefinedTerm/spec-driven-development]], making collaboration controllable and verifiable.
- A Korean practitioner account, [[BlogPosting/lessons-from-releasing-a-product-with-ai-agents]],
  concludes that real product work belongs to engineering rather than vibes, because a tool delivers
  value only once its output can be controlled and verified.
- A Red Hat Developer article, [[BlogPosting/the-uncomfortable-truth-about-vibe-coding]], uses the
  broad sense and sets its boundary by project lifetime and testability. If a unit or functional test
  can validate the output, the scope is small enough to vibe; if not, it needs a spec.

The first two treat vibe coding as the starting point of a transition, not as a category to defend
or widen. The third keeps it for small, test-validated units and prescribes a spec beyond that.

## What the coiner said

Karpathy's own statements do not settle the question either way. Replying to Willison's
March 2025 article, as recorded on [[DefinedTerm/vibe-coding]] and [[DefinedTerm/semantic-diffusion]],
he wrote that it will take some time to settle on definitions. He said he uses "vibe coding" for the
times he feels he has no idea what he is doing, but that in practice he rarely goes full out vibe
coding and more often still looks at the code.

A year later, as recorded on [[DefinedTerm/agentic-engineering]], he paired the term with a second
one. In that pairing, vibe coding raises the floor by letting almost anyone build software by
describing it, while agentic engineering extrapolates the ceiling. He added that vibe coding is fine for
prototypes and personal tools.

## Where the disciplined side's name split

The narrow reading needs a separate name for disciplined, reviewed, agent-assisted development, and
the grounding pages record several candidates for it. [[DefinedTerm/agentic-engineering]] reports
that Karpathy suggested "agentic engineering" in early February 2026. Osmani adopted that name for
what he had previously called "AI-assisted engineering". Willison had earlier proposed "vibe
engineering" for the same endpoint. According to that page, the term was offered precisely to stop
"vibe coding" being applied to two fundamentally different activities.

## The line blurring in practice

A 2026 account questions the narrow line from the disciplined side
rather than from the looser usage. In [[BlogPosting/vibe-coding-and-agentic-engineering-getting-closer]]
Willison reports that as coding agents became more reliable, he stopped reviewing every line they
write, including for production work. By his own operational test, that moves such work toward the
side of the line he had marked as irresponsible for software other people use.

He does not redefine the term to accommodate this. Instead, he compares trusting an agent to
depending on another team's service. He states the limit of that comparison himself: a team carries
accountability and reputation, and an agent carries neither. He names the risk as an element of the
normalization of deviance.

## What each answer protects

The pages frame the stakes differently depending on which answer they hold.

- **For the narrow reading**, the stake is keeping one useful word. Willison describes the looser
  usage as an instance of [[DefinedTerm/semantic-diffusion]], a coined term's definition weakening as
  it spreads. He regrets losing what could have been "ONE piece of AI-related terminology with a
  clear, widely accepted definition". By May 2025 he conceded he had probably lost the argument,
  calling the effect "an unstoppable force".
- **For the umbrella reading**, the term names a family of practices. The survey's taxonomy
  describes that family along several axes, including how much a human reviews AI-generated code. On
  this reading, review is one variable within vibe coding rather than the line that defines it.
- **For the control-based accounts**, the question is less what the word means than when a project
  has outgrown it. Their boundary is set by maintainability, team scale or testability.

The grounding pages have not converged. Whether "vibe coding" should mean unreviewed code, any
prompt-driven development, or an early stage to be engineered past is still answered differently
depending on which page you read.
