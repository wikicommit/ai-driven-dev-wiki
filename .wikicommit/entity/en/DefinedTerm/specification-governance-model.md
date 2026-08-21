---
title: "Specification Governance Model"
type: "schema:DefinedTerm"
lang: en
tags: [governance, spec-driven-development, methodology, terminology]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2605.01160'
    hash: sha256:5df903e44f8c186d0b13aaf412c53e475ccd30551e159a2cbba53b5c0a79dd50
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A model proposed by Farrag (2026) that derives specification-driven development from Transaction Cost Economics, treating deterministic specifications as the contractual governance mechanism for non-deterministic code generators."
  termCode: "SGM"
  inDefinedTermSet: ""
---

The Specification Governance Model — abbreviated SGM — is a framework proposed in [[ScholarlyArticle/productivity-reliability-paradox]] that treats AI-mediated code production as a transaction between a human principal and an AI agent, and derives the appropriate level of specification discipline from Transaction Cost Economics. The paper claims it as the first formal economic theorisation of why [[DefinedTerm/spec-driven-development]] emerges as a rational governance response rather than a stylistic preference.

## Usage

**Three transaction attributes** supply the input. *Asset specificity*: code generated for a particular domain, architecture and codebase has limited value outside that context, and once integrated, switching generation methods incurs substantial adaptation costs — which in Transaction Cost Economics favours hierarchical governance, translated here as tighter specification constraints on the agent. *Behavioural uncertainty*: generators are non-deterministic, cannot guarantee adherence to unstated conventions, and introduce failure modes — hallucinated APIs, subtly incorrect edge-case handling, security vulnerabilities — that differ qualitatively from human programming errors, which favours mechanisms constraining behaviour ex ante over post-hoc review. *Frequency*: developers invoke AI assistants dozens to hundreds of times a day, which amortises the fixed cost of building governance structures and makes heavier upfront investment economically rational.

**Three propositions** follow. As asset specificity increases, optimal governance shifts from post-hoc review through constrained generation to specification-first governance. As behavioural uncertainty increases, the specification must move from natural-language description to executable contract. As frequency increases, rational investment in governance infrastructure increases. Taken together, the paper argues, high specificity plus high uncertainty plus high frequency makes heavy specification investment the economically optimal choice.

**Four governance mechanisms**, ordered by constraint intensity, are what the model prescribes in practice:

1. **Post-hoc review** — the default for Tier 1 tools, and in the paper's account the source of the "verification tax" behind the METR slowdown. Optimal only where asset specificity and behavioural uncertainty are both low, such as boilerplate and well-known patterns.
2. **Natural-language specification** — narrows the solution space before generation, but does not eliminate uncertainty because natural language is ambiguous and non-deterministic generators can read it differently across invocations.
3. **Executable contract** — a machine-verifiable specification such as tests, formal contracts, Gherkin scenarios, or structured spec documents. The paper names this the SGM-optimal mechanism for most Tier 2 and Tier 3 interactions.
4. **Constitutional governance** — a meta-specification establishing non-negotiable principles for testing approach, architectural conventions and language standards that govern all subsequent generation, with [[SoftwareApplication/spec-kit]]'s `/speckit.constitution` given as an instance. The most comprehensive governance, at the highest upfront cost.

A practical decision guide translates the propositions into three observable task characteristics — task scope (self-contained or cross-cutting), codebase context (greenfield or mature), and the criticality of the change.

The paper raises one qualification against its own theoretical base. Williamson's Transaction Cost Economics assumes agents with opportunistic self-interest; AI code generators have none. The behavioural uncertainty motivating governance here comes from non-determinism instead — variable outputs from identical prompts, unintended convention violations, failure modes arising from statistical properties of training data. The author argues the distinction is theoretically significant but functionally immaterial, since unpredictable output requiring verification is practically equivalent to unpredictable behaviour requiring monitoring, and flags a modified framework substituting "stochastic unreliability" for "opportunistic self-interest" as future work.

## Related Terms

The SGM is the paper's proposed response to the [[DefinedTerm/productivity-reliability-paradox]], and its governance tiers align with the integration tiers of the [[DefinedTerm/ai-augmented-methodology-taxonomy]]. Its two evaluated instantiations are [[SoftwareApplication/spec-kit]] at the feature level and the [[DefinedTerm/test-driven-ai-agent-definition]] pipeline at the agent-behaviour level.
