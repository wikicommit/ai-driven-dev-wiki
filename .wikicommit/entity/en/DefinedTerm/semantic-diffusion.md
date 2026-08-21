---
title: "semantic diffusion"
type: "schema:DefinedTerm"
lang: en
tags: [terminology]
sources:
  - type: url
    url: 'https://martinfowler.com/bliki/SemanticDiffusion.html'
    hash: sha256:e22226b9564c5e690e03148770f0f95360086ea75ffe6c520d12063a2644c4de
  - type: url
    url: 'https://simonwillison.net/2025/Mar/23/semantic-diffusion/'
    hash: sha256:bd8b1ebaf3a87c219b7e2befdbb0efc1bb8a0fcf0bb5870fcb6a2bd8732a81cb
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "The process by which a term coined by a person or group with a reasonably good definition is weakened as it spreads through the wider community, risking the loss of the definition and of the term's usefulness. Coined by Martin Fowler in 2006; Simon Willison invoked it in March 2025 to describe what was happening to the definition of vibe coding."
---

Semantic diffusion is [[Person/martin-fowler]]'s name for what happens when a word coined by a person or group, "often with a pretty good definition", then "gets spread through the wider community in a way that weakens that definition" — a weakening that, on his account, "risks losing the definition entirely - and with it any usefulness to the term." He set the term out in [[BlogPosting/semantic-diffusion]] in 2006, offering it as "yet another potential addition to our jargon" and describing its mechanism as "essentially a succession of the telephone game": a group other than the originators of a term starts talking about it without being careful to follow the original definition, is listened to by a further group that adds its own distortions, and after a few such hand-offs much of the key meaning is lost unless someone goes back to the originators.

## Usage

Fowler's own account identifies several conditions that make a term vulnerable. Diffusion tends to coincide with the hype phase of an idea, because popularity attracts followers who talk and teach about the term without going back to the source — which is why, he notes ironically, it is popular terms that suffer most. Desirability compounds it: a word that sounds good, such as "agile", is more attractive to adopt loosely than a deliberately unappealing one, and he credits Kent Beck with picking "Extreme Programming" partly because "extreme" is often used as a pejorative. Broad concepts are more exposed than concrete tools — Fowler contrasts agile's list of values and principles with a concrete tool, whose meaning is harder to weaken. He also argues the damage is usually not permanent, citing "object-oriented" and "patterns" as terms whose essential meaning was reasonably well understood again years later, and rejects abandoning a diffused term in favour of repeatedly re-articulating it and pointing to the people who understand its original meaning. The mechanism he offers for that recovery is the hype cycle turning on itself: "once the equally inevitable backlash comes we get a refocusing on the original meaning." His stated evidence is an absence rather than a case — writing that he cannot think of a term that lost its meaning entirely, while adding that he is sure it has happened, and explicitly discounting SOA on the grounds that he does not think there was ever a commonly agreed meaning for it to lose.

The concept was taken up in AI-assisted-development discourse in March 2025, when [[Person/simon-willison]] cited it while arguing that the definition of [[DefinedTerm/vibe-coding]] was being distorted to mean "any time an LLM writes code". Willison, who says he learned of the term that day from a Bluesky post, called what was happening to vibe coding "such a clear example of this effect in action", and reported that the same had happened over the preceding couple of years to his own coinage, prompt injection. He described the dilution as frustrating but apparently inevitable, restating Fowler's point that the more popular a term is, the higher the chance a game of telephone ensues.

Two further parts of his account bear on how a diffused term is meant to be handled. One is a claim about the medium: popular ideas "spread primarily though communication media that are more likely to lead to misunderstanding - such as writing," since many followers are not able to work directly with the originators and learn from them directly. The other is a limit on the remedy he prefers. Terms also *shift*, and Fowler holds that originators are responsible for saying so, "both by talking about the way the ideas evolve and by pointing to new people who are playing an active role in that evolution" — noting approvingly that the original seventeen authors of the agile manifesto "let the ship sail." His caution is that "there's a tricky balance between holding to a clear definition and dogmatism." His stated overall preference is nonetheless unambiguous — "I prefer the hype to ignorance", diffusion being in his view an inevitable consequence of ideas becoming popular — and he closes that "a good term is worth fighting for - particularly since the only bullets you need are words."

## Related Terms

The case that brought the term into this wiki's subject area is [[DefinedTerm/vibe-coding]]: Willison complained in March 2025 that its definition was "already being distorted to mean 'any time an LLM writes code'", as against the narrower meaning it was given when coined. See [[DefinedTerm/ai-assisted-software-development]] for the broader practice that looser reading collapses the term into.

Fowler's entry also records a named variant contributed by someone else: Holly Cummins coined "semantic inversion" for the case where a term ends up meaning the opposite of what it was coined to describe, his examples being "DevOps" becoming the name for a separated operations team and "Minimal Viable Product" being used for a $12M first release. That variant has no page here, its examples lying outside this wiki's subject area.
