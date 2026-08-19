---
title: "value stream management"
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
  description: "The practice of visualizing, analyzing, and improving the flow of work from idea to customer. DORA's 2025 research presents it not as a heavyweight process but as a set of four principles, and as the force multiplier that determines whether AI investment solves the right problems."
  termCode: "VSM"
---

Value stream management (VSM) is defined in [[Report/state-of-ai-assisted-software-development-2025]] as "the practice of visualizing, analyzing, and improving the flow of work from idea to customer." The report is careful about its weight: "It is not a heavyweight process, but a set of four principles for achieving the clarity needed to focus on improvements where they count most."

Its relevance to AI is the report's stronger claim. DORA states that VSM "is the force multiplier that turns AI investment into a competitive advantage, ensuring that this powerful new technology solves the right problems instead of just creating more chaos", and reports that teams who focus on understanding their value streams "dedicate significantly more of their time to valuable work."

## Usage

The mechanism the report describes is externalising the system. Holding a complex delivery system in one's head is "a huge mental drain" that gets in the way of seeing the bigger picture; when a team collectively maps the system, the details move "out of their heads and into a shared space", the structure and any hidden patterns become obvious, and it becomes possible to have a real conversation about what is and is not working. The map is meant to cover product discovery, design, development, testing, deployment and operations, so that the team can spot the real bottlenecks rather than optimize a part of the process that is not the constraint.

Scope is meant to be chosen rather than maximised. Mapping the whole system from concept to customer is the goal, but the report advises starting where the impact is greatest, after a high-level look to identify the primary constraint — and if a team's biggest challenges lie in product discovery, that may be the better place to begin. Its own default starting point, which it says DORA has used for years, is the scope from code commit to production, chosen because that part can most readily be standardized and tuned, and because it is where teams typically have the most agency to make immediate improvements; it contrasts this with discovery work, where the goal is optimizing for effectiveness. Completing that core scope, on the report's account, creates quick wins and the credibility to influence the wider system of product discovery and customer feedback.

The report names supporting practices around the map: measuring what matters, tracking lead time, process time and the ratio of value-add to wait time to establish a baseline and locate true constraints; treating the map as an ongoing cycle revisited regularly rather than a one-off exercise, and as the starting point for every improvement discussion; fostering a culture where teams are empowered to experiment, learn and adapt, with clear goals but autonomy over how to reach them and freedom from fear of reprisals; and building on a foundation of technical excellence, which it says is typically a well-designed internal platform.

The worked illustration the report gives for the AI connection is a team discovering through mapping that code reviews are a significant bottleneck, and deciding on that basis to apply AI to the code review process "rather than using AI to simply generate more code that will only exacerbate the bottleneck."

## Related Terms

The technical foundation the report says a smooth flow rests on is [[DefinedTerm/platform-engineering]]; the capability set it presents separately is the [[DefinedTerm/dora-ai-capabilities-model]].
