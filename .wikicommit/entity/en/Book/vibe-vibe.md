---
title: "Vibe Vibe"
type: "schema:Book"
lang: en
tags: [vibe-coding, tutorial, open-educational-resource]
sources:
  - type: url
    url: 'https://github.com/datawhalechina/vibe-vibe'
    hash: sha256:24c2d3605d61a510fa533468a180e476a5e0d054601e57c254a581af6438169f
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A free, open-source Chinese-language tutorial on AI-assisted programming (vibe coding) for learners with no programming background, published under the Datawhale community's GitHub organization. It aims to take a reader from having an idea to shipping a product, in four parts running from foundations to full-stack delivery."
  genre: "Technical tutorial"
---

Vibe Vibe is an open-source tutorial on [[DefinedTerm/vibe-coding]], written in Chinese under the
title 《Vibe Vibe —— 人人都能学会的 AI 编程（Vibe Coding）指南》 ("an AI programming guide anyone can
learn") and published from the Datawhale community's `datawhalechina` organization on GitHub. It is
read online at vibevibe.cn and licensed CC BY-NC-SA 4.0. Its stated audience is learners with no
programming background — students, entrepreneurs, working professionals, and also traditional
programmers wanting to learn a new way of working — and its stated aim is to carry them from "I have an
idea" to "I have built a product", so that anyone can become a builder.

The tutorial takes its framing from Andrej Karpathy's notion of vibe coding, which it glosses as a move
"from Coder to Commander": programming changes from writing code to conversational creation, directing
an AI in natural language. It describes itself as the first systematic open-source vibe coding
tutorial in China, motivated by what it sees as the fragmented state of Chinese-language learning
material at a time when vibe coding has become a global trend.

## Contents

The tutorial is organised into four parts, each aimed at a different reader:

- **Foundations** (基础篇) is an introduction for everyone. Its five chapters move from why now is the
  best time to program — including a chapter setting out vibe coding and "spec coding", and a comparison
  of tools such as Cursor, Windsurf, Bolt.new and Replit — through thinking like a product manager
  (minimum viable products, the questions of who the user is and what the pain point is), the craft of
  talking to an AI (prompt basics under the heading "Context is King", user journey maps, writing a
  first PRD, and prioritising features as P0, P1 and P2), a hands-on build of a personal tool in three
  rounds, and finally recovering from broken code, publishing to the web, security awareness, and the
  limits of what vibe coding can and cannot do.
- **Advanced** (进阶篇) is a sixteen-chapter guide to delivering a complete product "from zero to
  launch" while avoiding the usual pitfalls, covering among other things PRDs and document-driven
  development, environment variables and security, databases, testing, Git, serverless deployment
  and CI/CD, domains, server operations, SEO and analytics, and iterating on user feedback. It is built
  around a Next.js, React, TypeScript, Tailwind CSS, shadcn/ui, Drizzle ORM and PostgreSQL stack.
- **Practice** (实践篇) collects projects grouped by audience — humanities and business students,
  science and engineering students, working professionals — and an advanced set covering deployment,
  databases and authentication, AI agent development with RAG and MCP, full-stack projects, and
  workflow tools.
- **Curated articles** (优质文章篇) gathers company engineering blogs, podcasts, research reports,
  newsletters and developer communities for continued learning.

The README recommends different starting points by background: complete beginners start with the
first chapter, readers who have used ChatGPT but never built a project start with the chapter on
thinking like a product manager, and those with programming experience skim the foundations before
moving to the advanced part.

## Publication

Besides the hosted site, the repository ships a Dockerfile and Docker Compose configuration for
deploying the tutorial site privately on a local or intranet network. The project also announces a
forthcoming online edition built around a cloud IDE with Node.js, Python and Docker environments and
more than fifty preinstalled AI skills, so that learners can start without installing anything.
