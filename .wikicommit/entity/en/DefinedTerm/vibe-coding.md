---
title: "Vibe Coding"
type: "schema:DefinedTerm"
lang: en
tags: [llm, ai-assisted-programming, sandboxing, terminology]
sources:
  - type: url
    url: https://simonwillison.net/2025/Mar/19/vibe-coding/
    hash: sha256:653ba52b66ad62da601ae6fd257897841726d7ac6a07029edc6d0e1c5b12188f
  - type: url
    url: https://simonwillison.net/2025/Mar/23/semantic-diffusion/
    hash: sha256:472ba908e669a42742696d92e042aca8106e1995d7e09841e4452b160c3bb490
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "Building software with an LLM without reviewing the code it writes. Coined by Andrej Karpathy in early February 2025 for a deliberately unexamined, fast style of building, and argued here to be a narrow subset of AI-assisted programming rather than a synonym for it."
---

Vibe coding is the practice of building software with a large language model without reviewing the
code it produces. Andrej Karpathy, who coined the term in early February 2025, described it as
fully giving in to the vibes and forgetting that the code even exists — accepting every diff
without reading it, pasting error messages back in with no comment, and, where the model cannot
fix a bug, working around it or asking for random changes until it goes away. Writing in
[[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]], Simon Willison reduces the term to
a single operational test — whether the person building the software reviews the code — and argues
that it is already being stretched to cover every form of
[[DefinedTerm/ai-assisted-programming]], which both dilutes the term and misrepresents what
responsible AI-assisted work looks like.

## Usage
The term marks a boundary in how software is produced, not a particular tool or workflow. The same
model and editor can be used either way, and what decides the label is whether the resulting code
is read and understood before it is relied on. On Willison's account, code that an LLM wrote but
that has since been reviewed, tested, and understood well enough to explain to someone else is
ordinary software development, and the fact that an LLM produced it is immaterial.

Willison presents the narrow reading as a defence of the term rather than a criticism of it. He
argues that vibe coding lowers what is otherwise a steep initial barrier to programming, letting
people build custom tools for tedious tasks without a computer science degree or a bootcamp, and
that some of them will go on to become proficient developers. He also presents it as useful to
experienced developers as the best available way to build intuition about what LLMs can and cannot
do, reporting that he has published more than eighty experiments built this way. That figure and
that assessment are his own account of his own practice.

Within weeks of the term entering circulation the narrow reading was visibly losing ground. By late
March 2025 Willison described himself as losing the battle, saying he kept seeing the term used to
mean any time an LLM is used to write code, and named what was happening to it:
[[DefinedTerm/semantic-diffusion]], a term he had just learned for a coined word's definition
weakening as it spreads beyond the people who coined it. His diagnosis of the cause was that people
could not be trusted to read Karpathy's original post all the way to the end, where the scoping to
throwaway projects appears. Karpathy, replying to that article, wrote that it will take some time to
settle on definitions: he said he uses "vibe coding" for the occasions when he feels like the dog in
the "I have no idea what I'm doing" image, citing an iOS app he had built the night before, but that
in practice he rarely goes full out vibe coding — more often he still looks at the code, adds
complexity slowly, tries to learn over time how the pieces work, and asks clarifying questions.

## When It Applies
Willison sets out the conditions under which he considers vibe coding acceptable, addressed
explicitly to people new to building software:

- **Low stakes.** Weigh how much harm the code could cause if it has bugs or security
  vulnerabilities — damaged reputation, lost money, or worse — with particular care if other people
  will use it.
- **Secrets.** Anything shaped like a password or API key has to be handled deliberately, which
  means understanding how the code works rather than not reading it.
- **Data privacy.** Approach a tool with access to private data cautiously, and be sure whether
  there are paths by which that data could leave the machine.
- **Load on other services.** Code that makes requests to other platforms can raise their load and
  cost, so being a good network citizen is part of the judgment.
- **Metered spending.** Willison cites accounts of people vibe coding against an API with no
  billing limit and running up thousands of dollars in charges.

Two of these conditions cut against the practice's own premise: judging secret handling and data
egress requires understanding code that vibe coding leaves unread, so the technique is at its
safest where neither is in play. Willison's own mitigation for anything that others might use is
social rather than technical — check with someone more experienced before sharing it — and his
proposed design direction is a sandbox, as in [[SoftwareApplication/claude-artifacts]], which
constrains what unread code can reach. He notes that tools aimed initially at professional
developers, such as [[SoftwareApplication/cursor]], have far fewer such rails.

The definition given here rests on one practitioner's argued position, building on Karpathy's
coinage; the post is itself a response to the term being used more loosely elsewhere, so the narrow
reading should not be taken as settled or universal usage.

## Related Terms
- [[DefinedTerm/ai-assisted-programming]] — the broader practice this term is a subset of
- [[DefinedTerm/semantic-diffusion]] — the effect this term's own reception is offered as an example of
