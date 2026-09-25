---
title: "谈谈 AI 编程工具的进化与 Vibe Coding"
type: "schema:BlogPosting"
lang: en
tags: [ai-assisted-programming, context-engineering, coding-tools]
sources:
  - type: url
    url: 'https://guangzhengli.com/blog/zh/vibe-coding-and-context-coding'
    hash: sha256:1fb990c1b96d538c33025bac005806f001ffce5a54b8a29877454d271c67a3dd
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A Chinese-language personal blog post arguing that \"vibe coding\" should keep the narrow sense of Andrej Karpathy's original post — programming purely by conversation, without reading the code — and that ordinary AI-assisted programming is better called Context Coding, because beyond model capability its progress comes from better context engineering."
  author: ["guangzhengli"]
  datePublished: "2025-08-28"
---

"谈谈 AI 编程工具的进化与 Vibe Coding" (roughly, "On the evolution of AI programming tools, and vibe
coding") is a personal blog post published on guangzhengli.com on 28 August 2025. Its author, who
says they began using GitHub Copilot in 2023, used Cursor continuously from 2024 and had been using
Claude Code heavily for a few months before writing, argues that [[DefinedTerm/vibe-coding]] has
become a label for every way of writing code with AI, and that much of the current argument about it
comes from not separating two different practices.

The post keeps "vibe coding" for the sense of the Andrej Karpathy post it quotes, which it reads as
four points: forgetting that the code exists; fixing even small errors through the AI rather than by
hand; no longer reviewing what the AI writes and judging only the result; and accepting that this is
not bad, and fairly fun, for throwaway projects. For AI-assisted programming in general it proposes
the name [[DefinedTerm/context-coding]], and spends most of its length on that practice, reading the
history of the best-known coding tools as a history of [[DefinedTerm/context-engineering]].

## Key Points

- The author proposes "Context Coding" as a better name for AI-assisted programming than vibe coding,
  on the view that, with the model held fixed, every improvement in AI-assisted programming rests on
  passing the LLM more suitable context — whether through chat, RAG, rules or MCP.
- [[SoftwareApplication/github-copilot]]'s early success is attributed to being the first tool to
  bring code context together for the LLM — the code in the open editor window and the code around the
  cursor. Its early limits, as the author recalls them, were a model that still hallucinated heavily
  on code (GPT-3.5 at the time), a small context, no ability to edit code directly, and no view of any
  file other than the one open.
- [[SoftwareApplication/cursor]] is credited with indexing a project's entire codebase for semantic
  (vector) search through RAG, and with letting users attach files and folders to the context
  themselves; the author reads this fuller, more user-controlled context as why it overtook Copilot.
- [[SoftwareApplication/claude-code]] is described as feeding the model context generously: it first
  analyses a codebase's structure and technology stack, then retrieves code with Unix tools such as
  grep, find, git and cat rather than RAG. In the author's experience the two tools are similar on
  small and medium tasks, while on large tasks touching more than ten files Claude Code does far
  better, which the author attributes to Anthropic, as the model provider, being less constrained in
  how many tokens it spends.
- The author treats both sides of the RAG-versus-grep dispute as having a point, predicts that full
  AI IDEs will come to offer both kinds of retrieval, and argues that terminal tools such as Claude
  Code and Gemini CLI need not adopt RAG, because their strength also lies in scriptable workflows that
  integrate with codebases, MCP and CI/CD pipelines.
- Practical advice, drawn from the author's own practice: give the model what a new team member would
  need — the technology stack, the directory structure, what files are named and for what, common
  commands such as install, lint, test and build — in an instruction file such as GitHub Copilot's
  `.github/copilot-instructions.md` or Claude Code's `CLAUDE.md`. The author warns that such context
  is not better the more there is of it: information that goes stale without the file being updated,
  such as directory layouts or frequently refactored utilities, does more harm than leaving it out.
- For complex tasks the author suggests having the model split the work into subtasks recorded in a
  document, update that document as each one is finished, commit in small steps and delete the
  document at the end, and reports that this markedly reduces hallucination.
- Other sources of context the post recommends are current documentation passed in through MCP
  servers such as context7, and having the model add logging throughout faulty code as a stand-in for
  a debugger's view of inputs and outputs. It singles out Claude Code's built-in `/context` command,
  which shows how much of the context window each kind of content occupies and how much remains, as
  the first tool the author had seen expose context usage to the user.
- The author's own practice is mixed rather than agent-only: in serious engineering work, Cursor's Tab
  completion is what the author uses most, writing the layering and abstractions by hand and letting
  completion fill in the code, because in the author's experience LLMs remain poor at abstraction.
- On vibe coding proper, the post argues that for people without programming experience it introduces
  defects and security vulnerabilities in the short term and unmaintainable code and technical debt
  in the long term. It borrows the comparison of handing a child a credit card before explaining debt,
  and recounts an X user whose product, built entirely by vibe coding, was shut down days after the
  post announcing it drew attention: the product was attacked, its API key usage hit the maximum, and
  someone bypassed its subscription.
- On careers, the author states a pessimistic view: that most programmers work as translators of
  natural-language requirements into code, that LLMs can increasingly fill that role, and that the
  number of average programmers will shrink, while AI's leverage will make independent developers and
  small teams more common.

## Context

The post is one practitioner's opinion, grounded in the author's own use of the three tools it
discusses rather than in any measurement, and the author describes it as written in haste and full
of personal views. Its account of how Cursor's indexing works is a brief explanation in the author's
words; the post's reference list includes Cursor's security page on codebase indexing. On naming, the
post offers Context Coding as one of several names it considers better than vibe coding for AI-assisted
programming — alongside AI-assisted programming, AI Coding and Agents Coding — and states a personal
preference for it. For another piece of writing on where the boundary of vibe coding lies, see
[[BlogPosting/not-all-ai-assisted-programming-is-vibe-coding]].
