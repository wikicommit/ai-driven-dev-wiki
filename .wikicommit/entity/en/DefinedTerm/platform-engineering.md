---
title: "platform engineering"
type: "schema:DefinedTerm"
lang: en
tags: [metrics, ai-assisted-programming, terminology]
sources:
  - type: url
    url: 'https://services.google.com/fh/files/misc/2025_state_of_ai_assisted_software_development.pdf'
    hash: sha256:ebc154bec056cbe5e85fac4e00658b799f30fe548f4c46aea859cfa04f3fbd03
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The practice of building and running an internal platform for an organization's developers. DORA's 2025 research reports 90% adoption, finds that users perceive a platform as a single entity whose overall effectiveness matters more than any individual feature, and reports that a high-quality platform amplifies AI's effect on organizational performance."
---

Platform engineering, as [[Report/state-of-ai-assisted-software-development-2025]] treats it, is the practice of building and running an internal platform for an organization's own developers. The report's framing is that the question has moved on: "the conversation has shifted from if a platform is needed to how should a platform be built."

Its headline finding for this wiki's purposes is the interaction with AI: a high-quality platform "amplifies the effects of AI adoption on organizational performance", and "the positive impact of AI on organizational performance is strong when platform quality is high." The report's advice follows directly — prioritize and fund platform engineering initiatives, because "a poor developer experience and fragmented tooling may hamper the impacts of your AI strategy."

## Usage

The adoption figures the report gives are near-saturation. 90% of organizations have adopted at least one platform; 29% now use a multi-platform environment; 76% have at least one dedicated platform team, and more than a quarter of all respondents work in an organization with multiple platform teams. The report reads the multi-platform pattern not as redundant tooling but as organizations "moving past a one-size-fits-all model", creating federated and specialized platforms and teams for distinct domains and technology stacks — which shifts the leadership challenge "from simply 'having a platform' to 'governing a complex platform of platforms'", and which it says will benefit from the DORA capability of loosely coupled teams, with clear charters and interfaces so the ecosystem improves developer experience rather than creating new silos.

The report's substantive claim about how platforms are experienced is that quality is not decomposable: "users perceive their platform as a single entity; its overall effectiveness matters more than the quality of any individual feature in the platform." Its conclusion from that is that "a platform should be seen as a holistic entity that enables a great developer experience", and that organizations treating their platform "as an internal product designed to improve developer experience see significantly greater returns."

The trade-off is stated rather than hidden. The report recalls that DORA's 2024 research found platforms positively affecting organizational performance and productivity but with an increase in software delivery instability and a decrease in throughput; in 2025 it describes a platform as "an engine for managing risk, enabling speed and experimentation that corresponds to a small but credible increase in software delivery instability", which it characterises as "a manageable tradeoff for higher performance overall."

## Related Terms

Quality internal platforms are one of the seven capabilities in the [[DefinedTerm/dora-ai-capabilities-model]], and the report names a well-designed internal platform as the technical foundation that [[DefinedTerm/value-stream-management]] rests on. The practice whose returns it is reported to amplify is [[DefinedTerm/ai-assisted-software-development]].
