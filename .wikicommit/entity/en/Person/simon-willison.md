---
title: "Simon Willison"
type: "schema:Person"
lang: en
tags: [vibe-coding, ai-assisted-programming]
sources:
  - type: url
    url: 'https://simonwillison.net/2025/May/1/not-vibe-coding/'
    hash: sha256:4c658c9b0548d2a1a6e3cabefbb4299d17ce794ac693027d0c788262d01d7166
  - type: url
    url: 'https://arxiv.org/html/2510.17842v1'
    hash: sha256:787bc8812aeedac3e0166895e837e88ea57a2a23b1f901c470f6e3acf40fce47
  - type: url
    url: 'https://simonw.substack.com/p/vibe-engineering'
    hash: sha256:ef207bce62b3ace1d79b606bd1e4f06b56960f2525d3a90b75215d9f9c381aa2
  - type: url
    url: 'https://en.wikipedia.org/wiki/Vibe_coding'
    hash: sha256:e6ad2ca6bfbdd4ebfd679daf1a568bb11aba4e0d833594d90a8bcb226803d272
  - type: url
    url: 'https://simonwillison.net/2025/Mar/19/vibe-coding/'
    hash: sha256:e725441983198e989861ffd8eb4fbccea921fa47abf24f5644429df24f706ce5
  - type: url
    url: 'https://simonwillison.net/2025/Mar/23/semantic-diffusion/'
    hash: sha256:bd8b1ebaf3a87c219b7e2befdbb0efc1bb8a0fcf0bb5870fcb6a2bd8732a81cb
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Author of Simon Willison's Weblog, where he writes about LLMs and AI-assisted programming. He argues for a narrow reading of [[DefinedTerm/vibe-coding]], and coined the term [[DefinedTerm/vibe-engineering]] in October 2025."
---

Simon Willison writes Simon Willison's Weblog at simonwillison.net, covering LLMs and AI-assisted programming. He is a persistent advocate for a narrow reading of [[DefinedTerm/vibe-coding]] — that it means generating code with AI without caring about the code produced, rather than AI-assisted programming in general — a position he describes as "a hill I am willing to die on".

## Background

Willison had written on the meaning of vibe coding before his 1 May 2025 post, which links back to that earlier writing as his previous work on the subject. He publishes on the topics of AI, generative AI, LLMs and AI-assisted programming, is reachable on Mastodon, Bluesky and Twitter, and offers sponsors a monthly email digest of LLM developments.

His formulation of the distinction is widely quoted: "If an LLM wrote every line of your code, but you've reviewed, tested, and understood it all, that's not vibe coding in my book—that's using an LLM as a typing assistant." He is also cited for the practical objection that follows from it — that vibe coding your way to a production codebase is clearly risky, because most of the work software engineers do involves evolving existing systems, where the quality and understandability of the underlying code is crucial.

Willison has separately settled on a working definition of agents as "LLMs calling tools in a loop to achieve a goal," and maintains a collection of competing agent definitions from other parties, having noted OpenAI's much vaguer formulation — "a system that can do work independently on behalf of the user" — as an example of the waters being muddied.

His distinction between vibe coding and general AI-assisted programming has since been taken up in academic work. [[ScholarlyArticle/vibe-coding-ai-native-paradigm]] cites him as having distinguished the two, summarising his position as: when a developer uses an LLM but carefully reviews and understands every generated line of code, they are not vibe coding; vibe coding entails building software without reviewing the code the model writes.

## Works & Achievements

[[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]] (19 March 2025) is his earliest statement here of the distinction: that [[DefinedTerm/vibe-coding]] means "building software with an LLM without reviewing the code it writes", and that the definition was already escaping that intent six weeks after it was coined. It sets out his golden rule for production-quality AI-assisted programming — that he will not commit code to his repository if he could not explain exactly what it does to somebody else — while defending vibe coding itself as an access story for people without a computer science degree or a bootcamp, and as the best available way for experienced developers to build intuition about the tools, a use he backs with more than 80 published experiments of his own.

Four days later he attributed the term's broadening to [[DefinedTerm/semantic-diffusion]], [[Person/martin-fowler]]'s 2006 coinage, which he says he had learned of that day from a Bluesky post; he reports there that his own coinage prompt injection had suffered the same dilution over the preceding couple of years, and that the dilution of a popular term, while frustrating, appears to be inevitable.

[[BlogPosting/not-vibe-coding]] (1 May 2025) is his objection to two forthcoming books that use the term in their titles in a sense he considers the opposite of its meaning. Alongside the complaint he argues that vibe coding is for people who are not software developers, that a book teaching that audience to use these tools safely, effectively and responsibly could be a genuine bestseller, and that the opportunity has been lost to semantic diffusion.

In October 2025 he coined the term [[DefinedTerm/vibe-engineering]] for a more disciplined use of AI coding agents, encouraging experienced engineers to combine LLMs with best practices such as automated testing, planning, documentation, and code review to produce maintainable, production-quality software. He set the term out in [[BlogPosting/vibe-engineering]], where he lists the existing engineering practices he argues LLMs reward and defends the name as deliberately cheeky — noting he had previously tried and failed to make "AI-assisted programming" stick, and that he likes the self-contradiction between "vibes" and "engineering". He reports there that he had become one of the engineers running multiple coding agents at once, having been skeptical of the practice at first.
