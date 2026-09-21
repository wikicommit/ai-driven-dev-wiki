---
title: "4D-ARE: Bridging the Attribution Gap in LLM Agent Requirements Engineering"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, requirements-engineering, spec-driven-development]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2601.04556'
    hash: sha256:47686611cd9c576575a542851a7df72a328d486ff7ae3ce584ed719df20ad9f9
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A methodological proposal for specifying, at design time, what an LLM decision-support agent should reason about — organizing domain knowledge into four causally ordered dimensions and five specification layers that compile into system prompts — demonstrated through one industrial pilot and presented explicitly as preliminary."
  author: ["Bo Yu", "Lei Zhao"]
  datePublished: "2026-01-08"
  abstract: "The paper opens from a deployment in which an LLM agent with ReAct reasoning and full data access executed flawlessly but, asked why a completion rate was 80%, returned metrics instead of a causal explanation. It argues this reflects a gap between runtime reasoning frameworks, which determine how an agent thinks, and design-time specification, which determines what it should think about, and proposes 4D-ARE as a methodology for the latter."
  keywords: ["Agent Requirements Engineering", "LLM Agents", "Causal Attribution", "Goal-Oriented Requirements Engineering", "Prompt Engineering", "Decision Support Systems"]
---

This paper starts from a failure its authors describe as technically perfect. An LLM agent built to help bank managers review relationship-manager performance had access to all the relevant data and used ReAct-style reasoning; when a regional manager asked why one region's deposit completion rate was only 80%, it returned the rate, the visit frequency, the product penetration figure and the advice that the team should improve these metrics. The paper is not consistent about the episode's status: its abstract states "we deployed" such an agent, while the section that tells the story opens "consider a deployment scenario". The authors' diagnosis is that the fault was theirs rather than the framework's: the agent knew how to retrieve and reason, but nobody had specified what it should reason about.

From that they generalize the [[DefinedTerm/attribution-gap]] — decision-makers ask about outcomes, but what they are actually after is a causal chain connecting the outcome to something they can act on — and propose [[DefinedTerm/4d-are]] as a design-time methodology for closing it. The proposal has two parts: a four-dimensional structure for organizing what an agent should reason about (Results, Process, Support, Long-term), motivated from Pearl's causal hierarchy and control theory; and a five-layer architecture that turns that structure into concrete YAML artifacts which compile into components of the agent's system prompt.

The evaluation is a single industrial pilot: a Performance Attribution Agent for relationship-manager review at a commercial bank. The paper is unusually forthright about the weight this can bear. It labels itself a methodological proposal with preliminary industrial validation, marks the four-dimensional structure as motivated by theory but not derived from it, and states that its deployment observations should be treated as hypotheses for future investigation rather than validated findings.

One caveat governs every figure from that pilot and is easy to miss: the section reporting it opens by saying that, to protect sensitive business intelligence, the specific metrics and examples given are constructed for demonstration purposes while reflecting realistic patterns. The numbers below therefore illustrate what the method is claimed to do; they are not presented as measurements of it.

## Key Points

- The paper's framing claim is a division of labour: runtime reasoning frameworks answer how an agent should think during execution, and assume someone has already answered what it should think about. It argues that second question is the under-addressed one.
- It names the consequence of leaving it unanswered the "promptware crisis": agent development degrading into trial-and-error prompt engineering, with implicit knowledge living in developers' heads and agents failing in predictable ways — incomplete explanations, boundary violations, missed causal connections.
- The four dimensions are Results (observable outcome metrics), Process (controllable actions), Support (configurable resources) and Long-term (environmental context), with a stated causal direction: Long-term constrains Support, which enables Process, which produces Results.
- Attribution traces that chain backwards. The paper's principle of attribution completeness holds that a response is complete if and only if it addresses every dimension on the backward causal path from the one queried.
- The paper argues against both a three- and a five-dimension version: collapsing Support and Long-term would lose the distinction between what a decision-maker can change and what they must adapt to, while splitting Process into planning and execution would put two things operating at the same timescale in separate dimensions.
- Agent authority is graduated by dimension: the agent may interpret and make specific recommendations for Process, only open-ended recommendations for Support, and for Results and Long-term provides no interpretation or recommendation at all.
- The five layers are Question Inventory (what the agent perceives), Attribution Model (how it traces causality), Data Mapping (what data it accesses), Dual-Track Logic (when to interpret versus recommend) and Boundary Constraints (what it must not do).
- On a constructed set of 20 representative queries, the authors report the 4D-ARE agent covering 3.8 of the four dimensions on average against the baseline's 1.2, identifying 4.2 causal factors against 1.5, producing 1.8 actionable recommendations against 0.3, and committing 0.1 boundary violations against 2.1 — figures that fall under the section's constructed-for-demonstration caveat.
- That comparison carries an explicit caveat from the authors: it was conducted by them on queries they constructed to demonstrate the method's effects, counted by a single rater with no inter-rater reliability assessment, and no statistical significance is claimed.
- Before Layer 5 constraints were added, pilot testing produced personnel recommendations, unfounded claims such as "this suggests management failure", and overconfident language; the authors report these were eliminated after boundary constraints were implemented.
- Implementation effort is reported as dominated by data mapping: Layer 3 at 60% against roughly 40% for the four conceptual layers combined — again a constructed figure rather than a measured one. The authors read it as meaning 4D-ARE front-loads specification work rather than reducing total effort.
- Two analysts independently building attribution models for the same question are reported to have produced identical primary attribution paths, 80% overlap in secondary factors, and the same boundary-constraint categories — offered as a sign the method is reproducible across practitioners, and subject to the same caveat.
- Three domain experts (a COO and two branch managers) reported the four-dimensional structure matched how they already thought; one is quoted saying "this is exactly how I think through performance problems—I just never wrote it down."
- A lesson the authors draw is that experts often cannot articulate their reasoning directly but can validate an attribution chain once it is put in front of them, which is how the method externalizes tacit knowledge.
- Another is that agents do not infer appropriate boundaries from positive examples alone, so explicit "must not" constraints are necessary rather than optional.

## Notes

The paper positions itself against six existing traditions rather than one, arguing in each case that the tradition solves an adjacent problem: runtime reasoning needs domain specification; Goal-Oriented Requirements Engineering was designed for deterministic code agents rather than probabilistic prompt-configured ones; knowledge engineering assumes knowledge can be made explicit where attribution logic is partly tacit; prompt engineering supplies technique without content; specification-driven development structures the development process without saying what domain knowledge an agent needs; and existing causal-attribution work explains agent behaviour at runtime rather than specifying it at design time. On the fifth of these it explicitly frames its own method as complementary — a practitioner could organize their process one way and specify the agent's domain knowledge another.

Its stated limitations are as broad as its claims are hedged. The pilot is one domain (financial services), one organization (a single commercial bank) and one agent type, with no demonstrated transfer to healthcare, manufacturing or retail. Attribution completeness and expert usability were assessed qualitatively rather than with validated instruments. The response examples used to contrast baseline against 4D-ARE were selected to illustrate that contrast rather than sampled systematically. And the sample sizes — three experts, two analysts — are, in the authors' own words, too small for statistical inference.

It appears as arXiv:2601.04556v1 [cs.SE], dated 8 January 2026, and is marked a preprint under review; both authors give Tencent affiliations.
