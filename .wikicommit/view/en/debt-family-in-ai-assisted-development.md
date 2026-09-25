---
title: "The debt family in AI-assisted development"
lang: en
kind: pattern
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"
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

Eight pages in this wiki name a kind of "debt" that AI-assisted or agentic development is said to accumulate: [[DefinedTerm/verification-debt]], [[DefinedTerm/cognitive-debt]], [[DefinedTerm/comprehension-debt]], [[DefinedTerm/trust-debt]], [[DefinedTerm/governance-debt]], [[DefinedTerm/prompt-debt]], [[DefinedTerm/fast-integration-debt]] and [[DefinedTerm/provenance-debt]]. They come from at least six separate framings: Koch's synthesis paper, Addy Osmani's keynote and a post of his, a separate post on parallel agents, a study of an undergraduate software engineering project, a column on agentic software engineering, and one multivocal literature review that names four of the eight. This page describes what recurs across them and where they diverge. It does not rank them or decide which is the right name for any of them.

## The eight cases

| Term | Named in | What is said to accumulate | Where the debt sits |
|---|---|---|---|
| [[DefinedTerm/verification-debt]] | Koch, [[ScholarlyArticle/agentic-agile-v]] | weak tests, hidden regressions, broad patches, unvalidated dependencies, undocumented behaviour, reviewer burden | in unverified output and the team's review load |
| [[DefinedTerm/cognitive-debt]] | Osmani's "Own the Outer Loop" keynote; called "comprehension debt" in a separate post on parallel agents | erosion of an engineer's own understanding of how to solve a problem | in the individual engineer |
| [[DefinedTerm/comprehension-debt]] | [[ScholarlyArticle/comprehension-debt-in-genai-assisted-software-engineering-projects]] | the gap between what a team knows about its codebase and what it needs to understand | in the team's collective cognition, explicitly not in the code |
| [[DefinedTerm/trust-debt]] | [[BlogPosting/stop-vibe-coding-embrace-new-software-engineering]] | code shipped faster than anyone can establish it should be trusted | in what nobody has established about the code |
| [[DefinedTerm/governance-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | a continuing oversight burden for incorporated LLM output, caused by hallucination and non-determinism | in oversight that does not end at merge |
| [[DefinedTerm/prompt-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | unclear, sensitive or undocumented prompts that reduce reproducibility | in prompts that shape code but are not kept like code |
| [[DefinedTerm/fast-integration-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | LLM output adopted without proper validation | in the gap between adoption speed and evaluation speed |
| [[DefinedTerm/provenance-debt]] | [[ScholarlyArticle/faster-code-deeper-debt]] | unclear ownership or missing attribution of generated code | in missing records, surfacing as legal or accountability questions |

The same review also names data debt and ethical debt among its six new categories; neither has a page of its own in this wiki, so they are not counted here.

## What recurs

### A rate mismatch as the mechanism

Four of the eight pages state the mechanism as one rate outrunning another, with generation as the fast side:

- [[DefinedTerm/verification-debt]]: teams accumulate it "if output volume grows faster than verification capacity".
- [[DefinedTerm/trust-debt]]: the speed of agent-generated code outruns the capacity to establish that it deserves trust; once generation stops being the bottleneck, human attention and review bandwidth become the binding constraint.
- [[DefinedTerm/fast-integration-debt]]: the problem originates in the gap between how quickly LLM output can be adopted and how quickly a developer can evaluate its downstream consequences.
- [[DefinedTerm/cognitive-debt]]: in the parallel-agents framing, letting agents generate faster than a person can understand accumulates debt that compounds across threads. [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] states the same speed asymmetry: a junior engineer can now generate code faster than a senior engineer can critically audit it.

The other four are not framed that way. [[DefinedTerm/comprehension-debt]] attributes the gap to AI tools reducing cognitive load, so that understanding which would have been built while doing the work is not built. [[DefinedTerm/governance-debt]] rests on properties of the model — hallucination and non-determinism — that make oversight continuing rather than a one-off cost. [[DefinedTerm/prompt-debt]] names a mismatch in how two kinds of artefact are treated, and [[DefinedTerm/provenance-debt]] a missing record of where code came from.

### Set against ordinary technical debt

Several pages define their term by what separates it from conventional technical debt, and the separating line is drawn in different places:

- [[DefinedTerm/comprehension-debt]]: distinct because it resides in the collective cognition of a team rather than in the codebase.
- [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]]: technical debt announces itself through mounting friction and is usually a conscious tradeoff with a known location, while comprehension debt breeds false confidence — the code looks clean and the tests are green.
- [[DefinedTerm/fast-integration-debt]]: the problem originates not in the quality of any particular artefact but in the adoption-versus-evaluation gap.
- [[DefinedTerm/provenance-debt]]: unlike code debt, which surfaces as maintenance friction, it surfaces as a legal or accountability question.
- [[DefinedTerm/governance-debt]]: scoped to the oversight burden of incorporated output, deliberately separated from existing work on technical debt in AI/ML systems.

### Stated as unmeasured

Four of the eight pages state outright that the debt they name is not measured:

- [[DefinedTerm/verification-debt]]: Koch offers no way to measure it directly and lists whether evidence bundles can reduce it as an open question.
- [[DefinedTerm/trust-debt]]: one author's framing, with no measurement of the debt and no method for observing it.
- [[DefinedTerm/fast-integration-debt]]: rests on practitioner reporting rather than measurement, identified inductively from grey literature.
- [[DefinedTerm/governance-debt]]: inductively derived from practitioner sources rather than measured.

[[ScholarlyArticle/faster-code-deeper-debt]], which names four of the eight, states the general form of this: neither literature it surveyed contained standardised benchmarks or datasets for evaluating technical debt in LLM-generated code. [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]] makes a related claim from practice: velocity metrics, DORA metrics, PR counts and coverage can all look healthy while the deficit stays invisible.

The other pages report evidence of a different kind without addressing measurement of the debt: [[DefinedTerm/cognitive-debt]] cites a randomized trial in which engineers who worked through AI scored lower on a comprehension quiz (50% against 67%); [[DefinedTerm/comprehension-debt]] describes four accumulation patterns observed in an undergraduate software engineering project; [[DefinedTerm/prompt-debt]] reports that well-structured prompts mitigated up to 87.1% of observed code smells in one study; and [[DefinedTerm/provenance-debt]] rests on one formal and one grey source out of the review's 104.

## Where the cases diverge

### Two things called "comprehension debt"

The name is used for two different concepts in this wiki. Osmani's usage — the gap between how much code exists and how much of it any human understands — is recorded on [[DefinedTerm/cognitive-debt]]: his keynote calls it cognitive debt, a separate post on parallel agents calls the same dynamic comprehension debt, and Osmani uses "comprehension debt" for it in [[BlogPosting/comprehension-debt-the-hidden-cost-of-ai-generated-code]]. [[DefinedTerm/comprehension-debt]] is the term as proposed in the undergraduate-project paper: a team's collective knowledge falling short of what maintaining the codebase requires. The first is framed around an engineer delegating to agents, the second around a team adopting generative AI tools; [[DefinedTerm/comprehension-debt]] lists [[DefinedTerm/cognitive-debt]] as a related term, and neither page treats the two as one concept.

### Where the debt is held

The cases split on whose ledger the debt is on. [[DefinedTerm/cognitive-debt]] places it in an individual engineer and [[DefinedTerm/comprehension-debt]] in a team. [[DefinedTerm/verification-debt]] places it in artefacts and review load, [[DefinedTerm/prompt-debt]] in inputs that are not under the controls applied to code, and [[DefinedTerm/provenance-debt]] in records that do not exist. [[DefinedTerm/governance-debt]] places it in the future: its defining feature is that the burden does not end at merge.

### One causes another

Only one causal link between terms is stated in the grounding pages. [[ScholarlyArticle/faster-code-deeper-debt]] describes a domino effect in which fast-integration practices trigger cascading governance risks if left unmanaged; as [[DefinedTerm/fast-integration-debt]] and [[DefinedTerm/governance-debt]] relay the review's account, fast integration creates more code requiring oversight, which turns into governance debt and then increased long-term maintenance cost. The other pages relate their terms to neighbours as related concepts; [[DefinedTerm/trust-debt]], for instance, lists [[DefinedTerm/verification-debt]] as "the closely neighbouring cost of unverified output" without stating a causal order.

### What each source proposes in response

The responses the sources attach to their terms differ in kind, following where each places the debt:

- review of generated output as drafts — a human-in-the-loop model recommended in 58 of the review's 73 grey sources, for [[DefinedTerm/fast-integration-debt]];
- evidence proportionate to risk — Koch's risk-adaptive gates and evidence bundles, for [[DefinedTerm/verification-debt]];
- team practices rather than code changes — verification practices, structured retrospectives and active learning assessments, for [[DefinedTerm/comprehension-debt]];
- making prompts durable — templates, registries and versioned documentation, for [[DefinedTerm/prompt-debt]];
- asking where code came from — provenance review, for [[DefinedTerm/provenance-debt]];
- trust engineering — a three-dimensional bill of materials, named as a later subject of the column, for [[DefinedTerm/trust-debt]].

## Related pages

[[DefinedTerm/review-bottleneck]], [[DefinedTerm/the-70-percent-problem]], [[DefinedTerm/skill-atrophy]], [[DefinedTerm/automation-bias]], [[DefinedTerm/cognitive-surrender]]
