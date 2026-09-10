---
title: "Not all AI-assisted programming is vibe coding (but vibe coding rocks)"
type: "schema:BlogPosting"
lang: en
tags: [llm, ai-assisted-programming, software-engineering]
sources:
  - type: url
    url: https://simonwillison.net/2025/Mar/19/vibe-coding/
    hash: sha256:653ba52b66ad62da601ae6fd257897841726d7ac6a07029edc6d0e1c5b12188f
review_status: pending
generated_at: "2026-09-10"
generated_by: "claude-opus-5[1m]"
generated_with: "0.5.0"

properties:
  description: "Simon Willison argues that vibe coding should keep its original narrow meaning — building software with an LLM without reviewing the code — rather than expanding to cover all AI-assisted programming, and defends the narrow practice on its own terms."
  author: ["Simon Willison"]
  datePublished: "2025-03-19"
---

This post is a terminological intervention. Written roughly six weeks after Andrej Karpathy coined
[[DefinedTerm/vibe-coding]], it responds to the term being applied to all code written with AI
assistance, which the author argues both dilutes it and misrepresents what responsible
[[DefinedTerm/ai-assisted-programming]] actually involves. Its central move is to fix the term to
one observable criterion: vibe coding means building software with an LLM without reviewing the
code it writes.

Having narrowed the term, the post spends most of its length defending what it has narrowed. The
author is explicit that he does not want vibe coding to become a pejorative synonym for
irresponsible AI use. He argues it lowers a barrier to programming that is otherwise steep enough
to exclude people who have no computer science degree or bootcamp behind them, and that it is also
the best available way for experienced developers to build intuition about where LLMs succeed and
fail.

The final third turns practical. It sets out the conditions under which the author considers vibe
coding acceptable — low stakes, care with secrets and private data, awareness of load imposed on
other services, and hard billing limits — and identifies sandboxing as the design problem worth
solving, contrasting [[SoftwareApplication/claude-artifacts]] with less constrained tools such as
[[SoftwareApplication/cursor]].

## Key Points
- Vibe coding means building software with an LLM without reviewing the code it writes; this is the
  author's own operational restatement of Karpathy's coinage, offered because he judges the term to
  be drifting.
- Vibe coding is not the same thing as writing code with the help of LLMs, and treating the two as
  synonyms gives a false impression of what responsible AI-assisted programming can achieve.
- Code an LLM wrote that has been reviewed, tested, and understood well enough to explain to
  another person is software development, and the LLM's involvement in producing it is immaterial.
- The author will not commit code to his repository if he could not explain exactly what it does to
  somebody else — stated as his own golden rule for production-quality work, not as an established
  industry norm.
- Karpathy's original framing already scoped the practice to throwaway weekend projects rather than
  to production work; the post quotes it in full to make that scoping visible.
- Vibe coding is worth defending because it lets people without formal training build their own
  custom tools, and because it flattens the initial learning curve that keeps people out of the
  profession.
- It is also the best tool available for experienced developers to build intuition about LLM
  capabilities — supported by the author's report of having published more than eighty of his own
  vibe-coded experiments, which is his own experience rather than a measured result.
- Vibe coding is appropriate only for low-stakes projects, and the harm a bug or vulnerability
  could cause matters more once other people use the software.
- Secrets and private data are the hardest constraints to satisfy, because judging whether either
  is safe requires understanding code that vibe coding leaves unread.
- Usage-metered APIs are a specific financial hazard; the author cites accounts of large
  unintended charges rather than incidents he reports firsthand.
- Safe vibe coding for beginners starts with a sandbox, and the sandboxing approach taken by Claude
  Artifacts is presented as an example worth following, with its restrictiveness acknowledged as a
  real cost.
- The author expects, and hopes for, substantial further innovation in tooling that lets people
  build custom tools productively and safely.

## Context
The post belongs to a series the author maintains on his own use of LLMs, and it explicitly
positions itself as narrower than his broader writing on the subject: he notes having described his
own working process elsewhere, and says vibe coding describes only a small subset of that approach.
Its argument is definitional rather than empirical — the evidence offered is the author's own
practice and Karpathy's original wording, not measurement — and it concedes that the looser usage
it objects to is already widespread in press coverage and online discussion. Its caveat to
beginners is characteristically social rather than technical: check with someone more experienced
before releasing anything others will use.
