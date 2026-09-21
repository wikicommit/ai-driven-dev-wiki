---
title: "AI-assisted Coding과 개발 생산성 향상 (부제: 실리콘밸리 개발자가 바라보는 AI 생산성 툴 및 개발 방식의 변화)"
type: "schema:BlogPosting"
lang: en
tags: [ai-assisted-programming, coding-tools, developer-productivity]
sources:
  - type: url
    url: 'https://devocean.sk.com/blog/techBoardDetail.do?ID=166591&boardType=techBlog'
    hash: sha256:63c9e8fe888606a826c1ab9e6bbdfd8373e6dcefdf4552ea8fd1aaadb6af7130
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A write-up on SK's DEVOCEAN blog of a March 2024 internal SK planet seminar on AI-assisted coding, arguing that the development lifecycle changes shape once an AI bot sits between requirements and code, that prompts become the new source code, and that the traits wanted from a coding bot are those wanted from a good developer."
  author: "josephyang"
  datePublished: "2024-07-30"
  publisher: "DEVOCEAN"
---

A Korean-language post on DEVOCEAN, SK's developer community site, summarising a talk given in March
2024 at Data & Tech Committee, SK planet's monthly internal technical sharing programme. The post is
an editor's write-up rather than the speaker's own text, published with the speaker's permission.
It surveys the generative-AI tooling available to developers at that time — GitHub Copilot at
length, ChatGPT-4's GPT Store and Code Interpreter, and a broader landscape drawn from a third-party
survey of generative-AI tools — and reports what the speaker learned about their effect on
productivity from contacts in Silicon Valley as well as from their own use.

Its substantive argument concerns how the shape of development changes. The post names the
pre-generative-AI cycle the "existing" development method, iterated agilely in sprints, and sets
against it an "AI-based" method in which an AI bot intervenes immediately after requirements and
produces code together with the human, with review and deployment following as before. From that it
draws the claim the post is built around: that the commands and conversation a human gives the bot
will themselves become the new source code, and that directly reading source code in the older sense
will become progressively rarer.

The post also offers a framing for what a coding bot should be like. The speaker lists the traits
developers would want — concise, reliable, inquisitive, self-aware, personalised — and observes that
these are the same traits wanted in a good human developer, with inquisitiveness meaning a bot that
asks back to understand the problem rather than simply executing the instruction. The speaker's
reading is that the coding bots of the time leaned toward the first two while the rest did not yet
seem to work well, and expects them to follow, much as a junior developer improves over time. The post closes on
generative-AI litigation and regulation, and on what the speaker expects of developer careers.

## Key Points

- The post distinguishes an "existing" development lifecycle from an "AI-based" one in which an AI
  bot intervenes directly after requirements and produces code alongside the human, with review and
  deployment unchanged.
- It argues that future source code will be the instructions and conversation a human gives the
  coding bot, and that developers will inspect source code in the older sense less and less.
- It proposes five traits wanted from a coding bot — concise, reliable, inquisitive, self-aware,
  personalised — and notes they are the same traits wanted from a good human developer, judging that
  bots of the time leaned toward the first two while the rest did not yet seem to work well, and
  expecting them to follow in time.
- It characterises the coding bot of the time as resembling a junior developer with a good attitude
  who occasionally lies, and argues that giving precise instructions and properly verifying output
  becomes the more important skill.
- It predicts that clear understanding of programming syntax will matter less than the ability to
  converse with a coding bot, and that coding may become a skill at roughly the level spreadsheets
  are today — useful to know rather than a specialism.
- The productivity claims are reported secondhand from the speaker's contacts: the head of a startup,
  himself a former developer, who funded enterprise Copilot licences for his engineers for about six
  months reported clearly improved productivity,
  especially among junior developers, and planned to run a second AI tool alongside it — one for
  code generation, another for unit tests — to avoid what felt like a feedback loop from relying on
  a single tool.
- It notes that developer productivity has no single definition, listing reduced coding time,
  improved code quality, better developer experience and improved coding skill as candidates.
- It raises generative-AI litigation — over unlicensed code reuse, training images, hallucinated
  output and news content — as an area where regulation has not kept pace, and names labour-market
  displacement as a further concern.
- The speaker's career advice is that problem definition, communication and leadership matter more
  than being strongly technology-oriented, since technology keeps changing.

## Context

The post is a dated snapshot rather than a current account: the talk was given in March 2024 and the
post says so explicitly, noting for instance that GPT-4o was not covered because it postdated the
talk. Its tool descriptions are of that moment — Copilot licence tiers and their feature
differences, Copilot Chat as a Copilot X feature released at the end of 2023, GitHub's shift from
describing Copilot as an AI pair programmer to an AI-powered developer platform — and the post's own
remark that about a third of the surveyed generative-AI tools had shut down by the time of the talk
is a fair indication of how quickly that layer moved.

The article draws its tool categories from a third-party survey of the generative-AI landscape,
which it restates, and points readers to a published piece on measuring Copilot's productivity
impact while explicitly skipping its detail. Its own productivity evidence is secondhand: what the
speaker was told by Silicon Valley contacts and what the speaker observed personally, alongside
figures the post relays from others, rather than a study the post conducted.
