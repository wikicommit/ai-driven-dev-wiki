---
title: "DORA AI Capabilities Model"
type: "schema:DefinedTerm"
lang: en
tags: [ai-assisted-programming, metrics]
sources:
  - type: url
    url: 'https://services.google.com/fh/files/misc/2025_state_of_ai_assisted_software_development.pdf'
    hash: sha256:ebc154bec056cbe5e85fac4e00658b799f30fe548f4c46aea859cfa04f3fbd03
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "DORA's model of seven organizational capabilities its 2025 research found to amplify the benefits of AI adoption, spanning technical and cultural aspects: a clear and communicated AI stance, healthy data ecosystems, AI-accessible internal data, strong version control practices, working in small batches, user-centric focus, and quality internal platforms."
---

The DORA AI Capabilities Model is a set of seven organizational capabilities that DORA's 2025 research found to amplify the benefits of AI adoption. It is introduced in [[Report/state-of-ai-assisted-software-development-2025]] as DORA's first such model, and its purpose is stated as going "beyond questions of who is adopting AI and how they're using it, to investigate the conditions in which AI-assisted software developers observe the best outcomes."

The seven capabilities, which the report says encompass "both technical and cultural aspects of an organization", are: a **clear and communicated AI stance**, **healthy data ecosystems**, **AI-accessible internal data**, **strong version control practices**, **working in small batches**, a **user-centric focus**, and **quality internal platforms**.

## Usage

The model's claim is specifically about interaction, not about main effects. The report describes hypothesizing a wide range of candidate capabilities from 78 in-depth interviews, expert opinion and previous DORA research, narrowing to 15 candidates for the survey, of which seven "showed substantial evidence of an interaction with AI use. That is, when teams paired these capabilities with AI adoption, the difference AI made across important outcomes was amplified."

The best-documented of the seven in the report is the **clear and communicated AI stance**, defined as "the comprehensibility and awareness of an organization's official position on how its developers are expected and permitted to use AI-assisted development tools". It is measured as a single factor from four indicators: how far AI use feels expected at work, how far the organization supports developers experimenting with AI, how clear it is which AI tools are permitted, and how directly the organization's AI policy applies to the respondent. The report's summary of what that adds up to is an organization that "encourages and expects AI use by its developers, supports its developers' experimentation with AI at work, and makes explicit which AI tools are permitted and the applicability of their AI policy for their staff."

For that capability the report states, "with a high degree of certainty", that AI adoption's positive benefits depend on organizations having a clear and communicated AI stance: where they do, AI's positive influence on individual effectiveness is amplified, its positive influence on reported organizational performance is amplified, and its neutral effect on friction "is made beneficial and shown to decrease friction". Separately, and explicitly "with a lesser degree of certainty", it reports that in the presence of such a stance AI's positive influence on software delivery throughput is amplified. Across the accompanying figures the size of AI's effect rises as the stance moves from extremely low to extremely high.

DORA presents the model as provisional. It says it will "continue validating, revising, and refining the DORA AI Capabilities Model with further research", as it has with the DORA Core Model, and that it is eager to share future iterations with the DORA community — so the seven capabilities should be read as an inaugural set rather than a settled framework.

## Related Terms

Two of the seven capabilities have their own coverage here: [[DefinedTerm/platform-engineering]] for quality internal platforms, and — as the report's separate force-multiplier finding rather than one of the seven — [[DefinedTerm/value-stream-management]]. The practice the model is about amplifying is [[DefinedTerm/ai-assisted-software-development]].
