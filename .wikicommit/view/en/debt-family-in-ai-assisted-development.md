---
title: "The debt family in AI-assisted development"
lang: en
kind: pattern
review_status: pending
generated_at: "2026-09-27"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"
derived_from:
  - path: .wikicommit/entity/en/DefinedTerm/verification-debt.md
    source_commit: 85965d4810db6ca0ab5d75ba68b7a03eeaa9f1ea
  - path: .wikicommit/entity/en/DefinedTerm/cognitive-debt.md
    source_commit: b0cc6ca63c7e8c23683ba90cc3b5cf0b4690d315
  - path: .wikicommit/entity/en/DefinedTerm/comprehension-debt.md
    source_commit: 59f94553fa52912f703987f31c807ff6a3208a7d
  - path: .wikicommit/entity/en/DefinedTerm/trust-debt.md
    source_commit: 07f44d78c36c0f3ef8211927eac4fa818f178ac1
  - path: .wikicommit/entity/en/DefinedTerm/governance-debt.md
    source_commit: 67eb2a7e7aeea32abb49ca81daa984b78b394440
  - path: .wikicommit/entity/en/DefinedTerm/prompt-debt.md
    source_commit: 67eb2a7e7aeea32abb49ca81daa984b78b394440
  - path: .wikicommit/entity/en/DefinedTerm/fast-integration-debt.md
    source_commit: 67eb2a7e7aeea32abb49ca81daa984b78b394440
  - path: .wikicommit/entity/en/DefinedTerm/provenance-debt.md
    source_commit: 67eb2a7e7aeea32abb49ca81daa984b78b394440
  - path: .wikicommit/entity/en/ScholarlyArticle/faster-code-deeper-debt.md
    source_commit: 67eb2a7e7aeea32abb49ca81daa984b78b394440
  - path: .wikicommit/entity/en/BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code.md
    source_commit: ef2531ca21f1030c853bca7e560613f050793160
---

Eight pages in this wiki name a kind of "debt" said to accumulate in AI-assisted or agentic software development: [[DefinedTerm/verification-debt]], [[DefinedTerm/cognitive-debt]], [[DefinedTerm/comprehension-debt]], [[DefinedTerm/trust-debt]], [[DefinedTerm/governance-debt]], [[DefinedTerm/prompt-debt]], [[DefinedTerm/fast-integration-debt]] and [[DefinedTerm/provenance-debt]]. Four of them come from a single multivocal literature review, [[ScholarlyArticle/faster-code-deeper-debt]]; the other four come from a synthesis paper by Koch, talks and posts by Addy Osmani, a study of an undergraduate software engineering project, and the opening instalment of one author's column. This page describes the shapes that recur across the eight and the places where they come apart. It does not rank the terms or decide which name is the right one for any of them.

## The eight cases

| Term | Where the wiki records it | What is said to accumulate | Whose ledger it is on |
|---|---|---|---|
| [[DefinedTerm/verification-debt]] | Koch, [[ScholarlyArticle/agentic-agile-v]] | weak tests, hidden regressions, broad patches, unvalidated dependencies, undocumented behaviour, increased reviewer burden | the team's unverified output and review load |
| [[DefinedTerm/cognitive-debt]] | Osmani's "Own the Outer Loop" keynote; a separate post on parallel agents; [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] | erosion of an engineer's own understanding of how to solve a problem | the individual engineer |
| [[DefinedTerm/comprehension-debt]] | [[ScholarlyArticle/comprehension-debt-in-genai-assisted-software-engineering-projects]] | the gap between what a team knows about its codebase and what it needs to understand to maintain it | the team's collective cognition, explicitly not the code |
| [[DefinedTerm/trust-debt]] | [[BlogPosting/stop-vibe-coding-embrace-new-software-engineering]] | code shipped faster than anyone can establish it deserves trust | what nobody has established about the code |
| [[DefinedTerm/governance-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | a continuing oversight burden for incorporated LLM output, caused by hallucination and non-determinism | oversight that does not end at merge |
| [[DefinedTerm/prompt-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | unclear, sensitive or undocumented prompts that reduce reproducibility and code quality | prompts that shape code but are not kept like code |
| [[DefinedTerm/fast-integration-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | LLM output integrated without proper validation | the gap between adoption speed and evaluation speed |
| [[DefinedTerm/provenance-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | unclear ownership or missing attribution of generated code | missing records, surfacing as legal or accountability questions |

The same review names two further new categories, data debt and ethical debt. Neither has a page of its own in this wiki, so they are not counted among the eight.

## Recurring shapes

### One rate outrunning another

Four of the eight pages describe the mechanism as a rate mismatch, with generation or adoption on the fast side:

- [[DefinedTerm/verification-debt]] — teams accumulate it if output volume grows faster than verification capacity.
- [[DefinedTerm/trust-debt]] — the speed of agent-generated code outruns the capacity to establish that the code deserves trust; once generation stops being the bottleneck, human attention and review bandwidth become the binding constraint.
- [[DefinedTerm/fast-integration-debt]] — the problem originates in the gap between how quickly LLM output can be adopted and how quickly a developer can evaluate its downstream consequences.
- [[DefinedTerm/cognitive-debt]] — in the parallel-agents post, letting agents generate faster than a person can understand accumulates debt that compounds across threads. [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] states the same asymmetry as an inversion: a junior engineer can now generate code faster than a senior engineer can critically audit it.

The other four are not framed as a race between two rates. [[DefinedTerm/comprehension-debt]] attributes the gap to AI tools reducing cognitive load, so that understanding which would have been built while doing the work is not built. [[DefinedTerm/governance-debt]] rests on properties of the model — hallucination and non-determinism — which make oversight continuing rather than a one-off cost. [[DefinedTerm/prompt-debt]] names a mismatch in how two kinds of artefact are treated, and [[DefinedTerm/provenance-debt]] a missing record of where code came from.

### Defined against ordinary technical debt

Four of the grounding pages define a term partly by what separates it from conventional technical debt, and each draws the line in a different place:

- [[DefinedTerm/comprehension-debt]] — it resides in the collective cognition of a team rather than in the codebase.
- [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] — technical debt announces itself through mounting friction and is usually a conscious tradeoff with a known location; comprehension debt breeds false confidence, because the code looks clean and the tests are green.
- [[DefinedTerm/fast-integration-debt]] — the problem originates not in the quality of any particular artefact but in the gap between adoption and evaluation.
- [[DefinedTerm/provenance-debt]] — code debt surfaces as maintenance friction, while this surfaces as a legal or accountability question.

[[DefinedTerm/governance-debt]] draws a different line: it is scoped to the oversight burden of incorporated output, and deliberately separated from the existing literature on technical debt in AI and ML systems rather than from conventional technical debt.

### A cost that arrives later

Four grounding pages — three of the eight term pages and Osmani's post — stress that the cost is not visible when the code goes in:

- [[DefinedTerm/fast-integration-debt]] — a practitioner account in which velocity metrics looked excellent during a sprint and the bug reports arrived weeks later, in edge cases the AI had not considered.
- [[DefinedTerm/governance-debt]] — its defining feature is that the burden does not end at merge.
- [[DefinedTerm/provenance-debt]] — the cost is deferred to the point where someone needs to establish who is answerable for a piece of logic or under what terms it may be distributed.
- [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] — the codebase looks clean and the tests are green right up until the reckoning arrives.

### Stated as unmeasured

Four of the eight pages say outright that the debt they name is not measured:

- [[DefinedTerm/verification-debt]] — Koch offers no way to measure it directly, and lists whether evidence bundles can reduce it as an open question.
- [[DefinedTerm/trust-debt]] — one author's framing, with no measurement of the debt and no method for observing it.
- [[DefinedTerm/fast-integration-debt]] — identified inductively from grey literature and resting on practitioner reporting rather than measurement.
- [[DefinedTerm/governance-debt]] — inductively derived from practitioner sources rather than measured.

[[ScholarlyArticle/faster-code-deeper-debt]] states the general case: neither literature it surveyed contained standardised benchmarks or datasets for evaluating technical debt in LLM-generated code. [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] makes a related claim from practice — velocity metrics, DORA metrics, PR counts and coverage can all look healthy while the comprehension deficit stays invisible.

The remaining pages report evidence of other kinds without addressing measurement of the debt itself: [[DefinedTerm/cognitive-debt]] cites a randomized trial in which engineers who worked through AI scored 50% on a comprehension quiz against 67% for those who did not; [[DefinedTerm/comprehension-debt]] describes four accumulation patterns observed in an undergraduate project; [[DefinedTerm/prompt-debt]] reports a study in which well-structured, specific prompts mitigated up to 87.1% of observed code smells; and [[DefinedTerm/provenance-debt]] rests on one formal and one grey source among the review's 104.

## Where the cases come apart

### Two concepts called "comprehension debt"

The same name is attached to two different concepts. Osmani's usage — the gap between how much code exists and how much of it any human understands — is recorded on [[DefinedTerm/cognitive-debt]]: his keynote calls it cognitive debt, the parallel-agents post calls the same dynamic comprehension debt, and [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] uses "comprehension debt" for it. [[DefinedTerm/comprehension-debt]] is the term as proposed in the undergraduate-project paper: a team's collective knowledge falling short of what maintaining the codebase requires. The first is framed around an engineer delegating to agents, the second around a team adopting generative AI tools. [[DefinedTerm/comprehension-debt]] lists [[DefinedTerm/cognitive-debt]] as a related term, and neither page treats the two as one concept.

### Where the debt is held

The eight differ on whose ledger the debt is on. [[DefinedTerm/cognitive-debt]] places it in one engineer and [[DefinedTerm/comprehension-debt]] in a team. [[DefinedTerm/verification-debt]] places it in output and review load, [[DefinedTerm/prompt-debt]] in inputs that are not under the controls applied to code, and [[DefinedTerm/provenance-debt]] in records that do not exist. [[DefinedTerm/trust-debt]] places it in what nobody has established about the code, and [[DefinedTerm/governance-debt]] in oversight that continues after the code is merged.

### How strongly the terms are backed

The four terms from [[ScholarlyArticle/faster-code-deeper-debt]] come with source counts, and those counts differ widely: [[DefinedTerm/governance-debt]] appears in 19 grey sources and no formal ones; [[DefinedTerm/fast-integration-debt]] in 13 grey sources and no formal ones; [[DefinedTerm/prompt-debt]] in 8 formal and 5 grey sources, and is reported as the primary source of LLM-specific debt in the formal literature; [[DefinedTerm/provenance-debt]] in one formal and one grey source. The other four terms each rest on one author's or one study's framing: a synthesis paper for [[DefinedTerm/verification-debt]], a keynote and posts for [[DefinedTerm/cognitive-debt]], an undergraduate-project study for [[DefinedTerm/comprehension-debt]], and a column's opening instalment for [[DefinedTerm/trust-debt]].

### One causal link

Only one causal link between terms is stated in the grounding pages. [[ScholarlyArticle/faster-code-deeper-debt]] describes a domino effect in which fast-integration practices trigger cascading governance risks if left unmanaged; as [[DefinedTerm/fast-integration-debt]] and [[DefinedTerm/governance-debt]] relay it, fast integration creates more code requiring oversight, which becomes governance debt and then increased long-term maintenance cost. The other pages relate their terms to neighbours only as related concepts — [[DefinedTerm/trust-debt]], for instance, lists [[DefinedTerm/verification-debt]] as the closely neighbouring cost of unverified output without stating a causal order.

### What each source proposes in response

The responses attached to each term differ in kind, following where each places the debt:

- [[DefinedTerm/fast-integration-debt]] — a human-in-the-loop model, recommended in 58 of the review's 73 grey sources: treating LLM output as drafts requiring review and refinement.
- [[DefinedTerm/governance-debt]] — ongoing developer training, documenting AI involvement in codebases, and prioritising long-term maintainability, alongside code quality tooling and multi-layered review.
- [[DefinedTerm/verification-debt]] — acceptance on evidence proportionate to risk, through the risk-adaptive gates and evidence bundles of [[DefinedTerm/agentic-agile-v]], and keeping tests inside the agent loop.
- [[DefinedTerm/comprehension-debt]] — practices rather than code changes: verification practices, structured retrospectives and active learning assessments.
- [[DefinedTerm/prompt-debt]] — making prompts durable: templates, structured prompts, prompt registries and versioned documentation.
- [[DefinedTerm/provenance-debt]] — provenance review, asking where the code came from, alongside governance checks and prompt documentation.
- [[DefinedTerm/trust-debt]] — trust engineering, with a three-dimensional bill of materials for the AI era named as a later subject of the column.
- [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] — no substitute: the post argues that tests and specs each have a ceiling as replacements for understanding, and that the comprehension work is the job.

## Related pages

[[DefinedTerm/review-bottleneck]], [[DefinedTerm/skill-atrophy]], [[DefinedTerm/automation-bias]], [[DefinedTerm/cognitive-surrender]], [[DefinedTerm/orchestration-tax]], [[DefinedTerm/vibe-coding]]
