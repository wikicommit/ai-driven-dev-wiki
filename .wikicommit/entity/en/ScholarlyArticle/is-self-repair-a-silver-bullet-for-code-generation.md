---
title: "Is Self-Repair a Silver Bullet for Code Generation?"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-generation, self-correction, execution-feedback, human-in-the-loop]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2306.09896'
    hash: sha256:17363bf30fafe6de7a50c6774def21c41d9bd0ed6d6b439b18b524bcd6f343ff
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An ICLR 2024 paper that measures self-repair for code generation with CodeLlama-13b-instruct, GPT-3.5 and GPT-4 on HumanEval and APPS, finding that once the cost of repair is counted the gains are often modest, and that the quality of the model's feedback on its own code is the bottleneck."
  author: ["Theo X. Olausson", "Jeevana Priya Inala", "Chenglong Wang", "Jianfeng Gao", "Armando Solar-Lezama"]
  keywords: ["self-repair", "code generation", "program repair", "feedback"]
---

The paper examines [[DefinedTerm/self-repair]], in which a model debugs and repairs its own code, and asks whether it actually beats simply sampling more programs when the extra model calls it needs are paid for out of the same budget. The authors note that existing studies of self-repair had been limited in scope, and that its efficacy depends not only on a model's ability to write code but on its ability to identify how its own code is wrong with respect to the specification — a stage they say no previous work had studied in detail.

They model self-repair as four stages — code generation, code execution against unit tests, feedback generation by a feedback model, and code repair — and call the tree of programs, feedback and repairs rooted in one specification a repair tree. To compare fairly, they adapt pass@k so that a repair tree counts as many samples as the programs it contains, and compare it against i.i.d. sampling without repair at the same number of programs. Separating the feedback step lets them swap in a stronger model's feedback, or a human's, and measure its effect in isolation. Experiments use CodeLlama-13b-instruct, GPT-3.5 and GPT-4 on self-contained Python problems from HumanEval and APPS.

## Key Points

- Self-repair is not a silver bullet: when the cost of repair is counted, the authors find several instances where i.i.d. sampling without repair achieves equal or higher pass rates, especially at small budgets.
- Gains are often modest and vary between and within datasets; on APPS, GPT-4 beats its no-repair baseline by up to 8% while GPT-3.5 sees marginal gains only at the largest numbers of initial samples.
- Self-repair is more likely to help when the budget is spent on a diverse set of initial programs rather than on many repair attempts per program; with GPT-4 on APPS, 10 initial samples with 1 repair each gave 1.05× the pass rate of pass@20, while 2 initial samples with 10 repairs each fell below pass@22 (0.97×).
- The authors hypothesize that self-repair is bottlenecked by the model's ability to give feedback on its own code: replacing a weaker model's feedback with a stronger model's beat both the no-repair baseline and plain self-repair in every configuration they tried, at all budgets.
- In a study with 16 participants on 40 failing GPT-4 programs, replacing GPT-4's own feedback with human feedback raised the fraction of repaired programs passing all tests by 1.58× (from 33.3% to 52.6%).
- A qualitative comparison found GPT-4's feedback far more often inaccurate than the participants' (32/80 versus 7/80), and that participants sometimes expressed uncertainty while GPT-4 never did.

## Notes

The authors list as limitations that their experiments bootstrap from one large pre-generated repair tree per task, which risks statistical artefacts; that self-contained Python tasks with executable unit tests differ from real-world software development, where specifications are often incomplete and tests are unlikely to exist for each snippet; and that their human study did not record how long participants took to debug. The paper was published as a conference paper at ICLR 2024; the authors are affiliated with MIT CSAIL and Microsoft Research.
