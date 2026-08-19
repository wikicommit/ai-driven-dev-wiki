---
title: "Not all AI-assisted programming is vibe coding (but vibe coding rocks)"
type: "schema:BlogPosting"
lang: en
tags: [vibe-coding, ai-assisted-programming, terminology]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/Mar/19/vibe-coding/'
    hash: sha256:e725441983198e989861ffd8eb4fbccea921fa47abf24f5644429df24f706ce5
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Simon Willison's post of 19 March 2025 arguing that vibe coding means building software with an LLM without reviewing the code it writes, and that applying the term to AI-assisted programming in general both dilutes it and misrepresents what responsible AI-assisted programming looks like — while defending vibe coding itself as valuable for beginners and for building intuition."
  author: ["[[Person/simon-willison]]"]
  datePublished: "2025-03-19"
---

In this post of 19 March 2025, [[Person/simon-willison]] argues that the definition of [[DefinedTerm/vibe-coding]] "is already escaping its original intent" barely six weeks after [[Person/andrej-karpathy]] coined it, and that applying the term to all code written with AI assistance "both dilutes the term and gives a false impression of what's possible with responsible AI-assisted programming." He quotes Karpathy's original tweet in full, emphasising the phrases "forget that the code even exists" and "It's not too bad for throwaway weekend projects", and states his own working definition: vibe coding means "building software with an LLM without reviewing the code it writes."

The post is not a criticism of vibe coding. Willison says he loves Karpathy's definition, notes that Karpathy is an experienced enough programmer to have no need of AI assistance and is using LLMs this way because trying wild ideas quickly is fun, and argues that for low-stakes projects and prototypes there is no reason not to let it rip. What he objects to is the term expanding to cover professional practice, and — separately — the risk of it hardening into a synonym for irresponsible AI use.

## Key Points

- The distinction is engagement with the code, not the tooling: if an LLM wrote the code and you then reviewed it, tested it thoroughly, and could explain how it works to someone else, "that's not vibe coding, it's software development," and the use of an LLM to support that is immaterial.
- Willison states a golden rule for production-quality AI-assisted programming: he will not commit code to his repository if he could not explain exactly what it does to somebody else.
- He grounds that rule in what he takes the job to be — producing code that demonstrably works, can be understood by other humans and machines, and supports continued development — while balancing performance, accessibility, security, maintainability and cost efficiency as trade-offs.
- He argues vibe coding's real value is access: everyone deserves to be able to automate tedious tasks with computers without a computer science degree or a bootcamp, and vibe coding "shaves that initial barrier down to almost flat."
- It is also, he argues, the best available tool for experienced developers to build intuition about what LLMs can and cannot do; he reports having published more than 80 experiments built this way.
- His conditions for when vibe coding is appropriate: keep projects low stakes; treat security carefully, watching for exposed secrets and for private data leaving the machine; be a good network citizen, since outbound requests raise load and cost on other services; and beware usage-billed APIs, citing horror stories of thousands of dollars in charges racked up without a billing limit.
- He recommends that a beginner who plans to share vibe-coded software with others check in with someone more experienced first.

## Context

Willison notes that the term had already been featured in the New York Times, Ars Technica and the Guardian by the time he wrote, and points readers to an earlier post of his own describing his full process for using LLMs on code, of which he says vibe coding describes only a small subset.

The post's closing section treats safe vibe coding as an unsolved design problem, starting from sandboxing. Willison praises [[SoftwareApplication/claude-artifacts]]' sandbox as making it very hard for a beginner to cause harm while also sharply limiting what such projects can do, contrasts it with [[SoftwareApplication/cursor]] — which he describes as initially intended for professional developers and as having far less safety rails — and says he hopes for "a cambrian explosion in tooling" that helps people build custom tools productively and safely.

Four days later Willison returned to the definition fight in different terms, attributing the term's broadening to [[DefinedTerm/semantic-diffusion]]; Karpathy replied to this post directly, agreeing that settling on definitions would take time.
