---
title: "State of AI-assisted Software Development 2025"
type: "schema:Report"
lang: en
tags: [ai-assisted-programming, research, metrics]
sources:
  - type: url
    url: 'https://services.google.com/fh/files/misc/2025_state_of_ai_assisted_software_development.pdf'
    hash: sha256:ebc154bec056cbe5e85fac4e00658b799f30fe548f4c46aea859cfa04f3fbd03
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "DORA's 2025 report, drawing on a global survey of nearly 5,000 technology professionals and more than 100 hours of qualitative data, whose central claim is that AI is an amplifier: it magnifies the strengths of high-performing organizations and the dysfunctions of struggling ones. It introduces the DORA AI Capabilities Model and seven team archetypes."
  author: ["Derek DeBellis", "Kevin M. Storer", "Nathen Harvey", "Matt Beane", "Rob Edwards", "Edward Fraser", "Benjamin Good", "Eirini Kalliamvakou", "[[Person/gene-kim]]", "Eric Maxwell", "Sarah D'Angelo", "Ambar Murillo", "Sarah Inman", "Daniella Villalba"]
  publisher: "[[Organization/dora]]"
  datePublished: "2025"
  abstract: "The report states that the central question for technology leaders in 2025 is no longer whether to adopt AI but how to realize its value, and that AI's primary role in software development is that of an amplifier — magnifying the strengths of high-performing organizations and the dysfunctions of struggling ones. Its stated key takeaway is that the greatest returns come not from the tools themselves but from a strategic focus on the underlying organizational system: the quality of the internal platform, the clarity of workflows, and the alignment of teams."
---

*State of AI-assisted Software Development 2025* is DORA's annual report, based on a global survey conducted between 13 June and 21 July 2025 with responses from nearly 5,000 technology professionals, together with more than 100 hours of qualitative data. Its framing claim is that the interesting question has moved: "the central question for technology leaders is no longer if they should adopt AI, but how to realize its value."

The answer the report gives is organizational rather than technical. Its stated key takeaway is that "AI is an amplifier": it "magnifies the strengths of high-performing organizations and the dysfunctions of struggling ones", and "the greatest returns on AI investment come not from the tools themselves, but from a strategic focus on the underlying organizational system: the quality of the internal platform, the clarity of workflows, and the alignment of teams." Without that foundation, the report argues, "AI creates localized pockets of productivity that are often lost to downstream chaos."

## Key Findings

- **Adoption is nearly universal, trust is not.** 90% of respondents use AI as part of their work and more than 80% believe it has increased their productivity — while 30% report little to no trust in AI-generated code. The report reads that gap positively, calling a "trust but verify" approach "a sign of mature adoption", and argues the conversation must shift from adoption to effective use, with training focused on teaching teams "how to critically guide, evaluate, and validate AI-generated work, rather than simply encouraging usage."
- **Throughput improved; instability did not.** The report records that AI adoption now improves software delivery throughput, which it calls "a key shift from last year", but that it still increases delivery instability — its reading being that "while teams are adapting for speed, their underlying systems have not yet evolved to safely manage AI-accelerated development."
- **The estimated effects, in order.** Comparing two people sharing the same traits, environment and processes, the report estimates the one with higher AI adoption reports higher individual effectiveness, higher software delivery instability, higher organizational performance, higher valuable work, higher code quality, higher product performance, higher software delivery throughput and higher team performance, with similar levels of burnout and friction. It notes explicitly that for instability an increase is *not* a desirable outcome, and that for burnout and friction a negative effect would be the desirable one.
- **Seven capabilities amplify AI's benefit.** The [[DefinedTerm/dora-ai-capabilities-model]] is the report's new contribution, identifying seven foundational practices "proven to amplify the positive impact of AI on organizational performance".
- **Seven team archetypes.** Cluster analysis produced seven profiles — foundational challenges, the legacy bottleneck, constrained by process, high impact low cadence, stable and methodical, pragmatic performers, and harmonious high-achiever — offered as a way to diagnose team health beyond delivery metrics, so leaders can tell "if a team is high-performing but burning out, or stable but stuck on legacy systems". The report cautions that the names and descriptions "are an interpretation of the data" and that a team may match a cluster's performance levels without the name fitting it.
- **Platform engineering is the foundation.** 90% of organizations have adopted at least one internal platform and a high-quality platform is reported to amplify AI's effect on organizational performance — see [[DefinedTerm/platform-engineering]].
- **Value stream management is a force multiplier.** [[DefinedTerm/value-stream-management]] is presented as what "turns AI investment into a competitive advantage, ensuring that this powerful new technology solves the right problems instead of just creating more chaos."

## Basis & Caveats

The evidence base is a self-reported global survey plus qualitative interview work, and the report is explicit that its estimates are associations between people, not causal claims about interventions: its effect statements are framed as what one would expect comparing two people who "share the same traits, environment, and processes" and differ in AI adoption, reported with 89% credible intervals. The team archetypes are described as an interpretation of cluster data rather than as categories a team must fall into.

The report is published by DORA, a Google Cloud research program, and its front matter lists platinum sponsors, gold sponsors, a premier research partner and research partners. Its own advice on how to use it is correspondingly hedged: "While every organization is unique, our findings provide a framework to inform your strategy and guide your teams. Use this research to form hypotheses, run experiments, and measure the results to discover what drives the highest performance in your specific context."

The report's Authors chapter credits fourteen people. The three listed first are Derek DeBellis, who has led DORA's research programme since 2022, Dr. Kevin M. Storer, who leads ethnographic research for the DORA team, and Nathen Harvey, who leads the team at Google Cloud; the remaining named authors are Matt Beane, Rob Edwards, Edward Fraser, Benjamin Good, Eirini Kalliamvakou, [[Person/gene-kim]], Eric Maxwell, Sarah D'Angelo, Ambar Murillo, Sarah Inman and Daniella Villalba. The foreword is Gene Kim's.
