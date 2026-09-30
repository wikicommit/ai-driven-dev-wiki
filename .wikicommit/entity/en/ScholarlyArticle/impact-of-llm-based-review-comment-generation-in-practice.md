---
title: "Impact of LLM-based Review Comment Generation in Practice: A Mixed Open-/Closed-source User Study"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, empirical-study, llm-as-a-judge]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2411.07091'
    hash: sha256:47096369e5a1f66e61a8c86b0c83b27dc3870d38290c956e48c1477fd5c8e108
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "A large-scale live user study at Mozilla and Ubisoft of RevMate, an LLM-based assistant that suggests code review comments, measuring how often reviewers accepted its comments, which kinds they accepted, what it cost them in time, and whether accepted comments led to revisions."
  author: ["Doriane Olewicki", "Leuson Da Silva", "Suhaib Mujahid", "Arezou Amini", "Benjamin Mah", "Marco Castelluccio", "Sarra Habchi", "Foutse Khomh", "Bram Adams"]
  datePublished: "2024-11-11"
  keywords: ["code review", "LLM-generated review comments", "user study", "retrieval-augmented generation", "LLM-as-a-Judge"]
---

This paper evaluates LLM-generated code review comments in a live setting rather than on a benchmark. It reports a large-scale empirical user study carried out inside the normal review environments of two organizations: Mozilla, whose codebase is open source, and Ubisoft, whose codebase is fully closed source. Participants were given access to RevMate, an LLM-based assistive tool that suggests review comments.

RevMate combines an off-the-shelf LLM with retrieval-augmented generation, to supply extra code and review context, and with [[DefinedTerm/llm-as-a-judge]], which auto-evaluates the generated comments and discards irrelevant ones. The study measures how often reviewers accepted the generated comments, which kinds of comment were accepted, how much extra time reviewers spent on them, and whether accepted comments led to revisions of the patch as often as human-written ones.

## Key Points

- Across more than 587 patch reviews provided by RevMate, 8.1% of generated comments were accepted by reviewers at one organization and 7.2% at the other.
- A further 14.6% and 20.5% of generated comments, respectively, were not accepted but were still marked as valuable as review or development tips.
- Refactoring-related comments were more likely to be accepted than functional comments (18.2% and 18.6% against 4.8% and 5.2%).
- The extra time reviewers spent inspecting generated comments or editing accepted ones yielded an overall median of 43 seconds per patch, which the authors judge reasonable.
- Accepted generated comments were about as likely to lead to a revision of the patch as human-written comments (74% versus 73% at chunk level).

## Notes

The evidence comes from two organizations and one tool, so the acceptance rates describe RevMate in those settings rather than LLM review assistants in general. The study's design, spanning an open-source and a closed-source organization, is what the title's "mixed open-/closed-source" refers to.
