---
title: "ZOZO"
type: "schema:Organization"
lang: en
tags: [ai-adoption, industry]
sources:
  - type: url
    url: 'https://techblog.zozo.com/entry/ai-development-two-commands'
    hash: sha256:58353a3fded13879de422c6b7cc6aff4012808394657a717d42726f5f81140df
  - type: url
    url: 'https://techblog.zozo.com/entry/cc-plugin-marketplace'
    hash: sha256:3ea931e475eb0d34cf89d80370d5fb142dc0684ce20d67ed208b882d87f015b1
review_status: pending
generated_at: "2026-09-22"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A company whose engineering blog reports that development AI agents are provided to all of its engineers under a company-wide program, with several hundred people using Claude Code. It measures its own adoption with an internal readiness score covering both individual use and whether AI-premised processes have been built into the organization, and its teams share development assets through a single Claude Code plugin marketplace as well as standardizing workflows within divisions."
  url: "https://corp.zozo.com/"
---

ZOZO appears in this wiki as an adopter of AI-driven development practice rather than as a vendor of tooling, and what is recorded here is how its own engineers describe the organization. Its tech blog reports that development AI agents — Claude Code among them — are provided to all of the company's engineers under a company-wide program, which the posts describe as based on a figure of 200 US dollars per person per month. The tools available under it are described as wide-ranging, naming [[SoftwareApplication/claude-code]], [[SoftwareApplication/openai-codex]], [[SoftwareApplication/devin]] and [[SoftwareApplication/cursor]]; Claude Code is reported as being used at a scale of several hundred people.

The company frames the resulting situation as a problem of variance rather than of uptake, and states it in two forms. Engineers who used the tools well were reported as raising their productivity across investigation, design, implementation and the organizing of review criteria, while the knowledge stayed inside individual practice and did not accumulate in a reusable form — so the organization's minimum level was slow to rise even as adoption spread. The same concern is stated at team level: as each team built up its own skills and agents, those assets stayed inside the team that made them, widening the gap between teams making progress with AI-assisted development and teams falling behind.

## Measurement

ZOZO defines an internal indicator for this called the All ZOZO AI Readiness Score, abbreviated AZARS. What distinguishes it, on the company's own account, is that it looks at two things rather than one: how far an individual has built AI into their work, and whether the organization has managed to encode AI-premised work processes into systems. The stated target is not merely the presence of people who are good at using AI, but a state in which anyone can begin AI-driven development at a consistent level from the same entry point.

## Activities & Products

Two responses to that concern are recorded, at different scales.

Within one division, the core systems division (基幹システム本部) built a pair of standard commands, `/dev-init` and `/dev-resume`, that combine Claude Code and Codex to cover design through implementation, review and — where applicable — front-end verification. The account of that work, including its rationale for pairing the two in a [[DefinedTerm/critical-dialogue-review]] loop, is on [[BlogPosting/ai-driven-development-two-commands]]. The commands are managed in a GitHub repository and can also be installed from a marketplace URL added via Claude Code's plugin command. The division's stated approach is to hold the user-facing surface at those two commands while continuing to update the prompts, Skills, review criteria and MCP integrations behind them, so that the organization can be moved to newer practice without engineers relearning an interface each time.

Across teams, a single [[DefinedTerm/claude-code-plugin-marketplace]] has been built and operated jointly since the second half of 2025, with the data systems department's MLOps block and the recommendation platform block among the teams involved. Plugins are held in per-team directories with a shared directory for cross-team ones, and skills, agents, scheduled Routines, loops and workflows invoked from GitHub Actions are all kept there — a placement the authors note settled on its own rather than by anyone's decision. After roughly ten months the account reports operation without major incident, and describes concrete reuse between teams as the main benefit, along with a shorter path for new members, who can now install and read working skills instead of building one from scratch. The account of that work is on [[BlogPosting/shared-claude-code-plugin-marketplace]].
