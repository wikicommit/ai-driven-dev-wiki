---
title: "Open Code Review：百万真实任务验证的确定性工程与 Agent 协同｜QCon 上海"
type: "schema:NewsArticle"
lang: en
tags: [qcon, code-review, ai-code-review, enterprise-ai-adoption]
sources:
  - type: url
    url: 'https://www.infoq.cn/article/owxMsObP9h1wFcRqW000'
    hash: sha256:60a6ed99d642c704fc28a825c63800527d10a8ac99ef3134464f957853cfb593
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A September 2026 InfoQ China announcement of a QCon Shanghai 2026 talk by the author of Open Code Review, on combining deterministic engineering with an agent to turn a general-purpose agent into a vertical code-review agent, validated on a million real tasks."
  datePublished: "2026-09-09"
  publisher: "InfoQ"
---

The article ("Open Code Review: deterministic engineering and agent collaboration validated on a million real tasks") is InfoQ China's announcement, dated 9 September 2026, of a talk in the "AI-driven software engineering" track at QCon Shanghai 2026, held 22–24 October. The speaker is a senior R&D engineer at Alibaba, the author of [[SoftwareApplication/open-code-review]] and the person responsible for AI code review across Alibaba Group. The article reproduces his talk outline, so what it reports is the speaker's own account of the project ahead of the talk.

The talk's thesis is that once AI coding is widespread, code review becomes the new efficiency bottleneck, and that a general-purpose agent cannot support production-grade review on its own: coverage, location accuracy and stability suffer, token cost and context grow, and prompt-driven design is not enough to solve what are engineering problems. The proposed answer is to converge a general agent into a vertical code-review agent by giving deterministic work to the engineering system and tasks that need semantic understanding to the model.

## Key Points

- The talk groups its engineering practice into five parts: divide-and-conquer concurrency to raise coverage, precise positioning to keep comments actionable, a rule template engine for stability and consistency, toolchain distillation for predictability and safety, and layered context management to reduce token use.
- Precise positioning is described as a three-level mechanism — file, then code segment, then line number — with hallucination interception to make sure every comment maps to real code.
- The rule template engine moves from prompt-driven to rule-driven review, injecting review context dynamically by file type and language.
- Toolchain distillation converges on high-frequency tool-call patterns drawn from real tasks, reducing exploratory calls and the uncertainty they bring.
- Layered context management divides context into a frozen zone of unchanging global background, a compressed zone of history that can be summarised, and an active zone holding the minimum context the current reasoning step needs.
- The talk reports validation on a million real tasks and usage data from more than 20,000 Alibaba developers, plus benchmark comparisons of precision, recall, token consumption and cost; the figures themselves are not given in the article.
- The open-source practice is presented as a complete "AI writes → AI reviews → AI fixes" loop.
- The speaker argues that adoption rate and the share of AI-authored comments stop working as metrics once AI participates deeply in development, and asks how a new evaluation system for AI review should be built.
- Named pain points are that every new file type, framework or business scenario needs a hand-written rule template, that the template engine is silent on patterns it has never seen where a general agent generalises zero-shot, and that the rule base itself decays as coding standards evolve.
- A second pain point concerns [[Dataset/aacr-bench]], the benchmark the speaker led in open-sourcing: its ground truth is a human annotation of one moment in time, so it drifts from production reality unless continuously updated, and each update is expensive to annotate.

## Context

This is a talk outline, so its claims — the million tasks, the developer count and the benchmark comparisons — are the speaker's own, and the benchmark results themselves are not given. Its argument for where an agent's judgment should and should not be used sits within the wider discussion this wiki covers under [[DefinedTerm/agentic-code-review]] and [[DefinedTerm/review-bottleneck]].
