---
title: "State of Code Developer Survey report 2026"
type: "schema:Report"
lang: en
tags: [ai-assisted-programming, developer-survey, code-quality, verification]
sources:
  - type: url
    url: 'https://www.sonarsource.com/state-of-code-developer-survey-report.pdf'
    hash: sha256:3d43f704cf1e52ecf4045d4342479248b68f557da49a051f79fb79b036967a0d
review_status: pending
generated_at: "2026-08-20"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Sonar's survey of 1,149 professional developers, finding that the explosion in AI-generated code has not yet produced the expected productivity gains but has instead created a verification bottleneck downstream of generation."
  publisher: "[[Organization/sonar]]"
  datePublished: "2026"
  abstract: "A quantitative online survey of 1,149 professional software developers, fielded throughout October 2025, on how AI is changing developer workflows — covering trust in AI-generated code, tool adoption, agentic AI use, toil, security concerns, technical debt, and differences by experience level and company size."
---

The State of Code Developer Survey report 2026 is a vendor survey published by [[Organization/sonar]], based on a quantitative online survey of professional software developers fielded throughout October 2025. Its stated headline finding is that "the explosion in AI-generated code hasn't led directly to massive and much-hyped productivity gains yet" and that instead "a verification bottleneck has emerged" — the framing that gives this wiki its [[DefinedTerm/verification-bottleneck]] page.

## Key Findings

**Use is routine; trust is not.** The report states that 72% of developers who have tried AI coding tools now use them every day, and that developers estimate 42% of the code they commit is AI-generated or assisted, up from 6% in 2023 on their own recollection and predicted to reach 65% by 2027. Against that, it reports that 96% of developers do not fully trust that AI-generated code is functionally correct.

**The bottleneck is the gap between that distrust and actual verification.** Despite the 96% figure, the report finds only 48% of developers always check their AI-assisted code before committing. It reports that 95% spend at least some effort reviewing, testing and correcting AI output, with 59% rating that effort "moderate" or "substantial", and that 38% say reviewing AI-generated code takes more effort than reviewing a human colleague's code against 27% who say it takes less. Its explanation for the cost is a single finding it calls critical: 61% agree that "AI often produces code that looks correct but isn't reliable", with the same 61% agreeing it "requires a lot of effort to get good code from AI".

**Impact concentrates upstream.** 89% report a positive impact on developer productivity and 70% on time-to-market, but the figures fall away further down the pipeline — 58% for code quality, 47% for both end-user experience and technical debt, 39% for defect rates, 34% for vulnerability rates and 25% for frequency of outages. The report's own reading is that shipping code which looks right but isn't reliable does not improve the user's experience or the long-term health of a codebase.

**Toil changed shape rather than shrinking.** 75% of developers agreed AI reduces time spent on toil work, yet the reported share of the work week spent on toil averaged 23–25% and stayed almost identical between frequent and infrequent AI users. The composition differed instead: less frequent AI users more often cited debugging poorly documented code (34%) and finding information or understanding existing systems (29%), while the most frequent users more often cited managing technical debt (44% against 34%) and correcting or rewriting code created by AI coding tools (25% against 15%).

**Technical debt moves in both directions.** 88% of developers reported at least one negative impact of AI on technical debt — led by code that looked correct but was not reliable (53%) and unnecessary or duplicative code (40%) — while 93% reported at least one positive impact, led by improved documentation (57%), improved test coverage and debugging (53%) and refactoring or optimizing existing code (47%). The report notes that "managing technical debt" was already the top source of toil, cited in the top five frustrations by 41% of developers.

**Security is the top concern and the least-automated task.** The most-cited concern was exposure of sensitive company or customer data (57%), followed by over-reliance on AI eroding the team's understanding of the codebase (53%) and deskilling (48%); introduction of new or subtle vulnerabilities was cited by 47%. Yet security vulnerability patching or remediation was the least common agentic use case at 28%, which the report presents as a gap between what developers need and what they use AI for. Organisational response was not settled: 37% reported being more rigorous about code security because of AI, 36% about code quality and 32% about compliance, with roughly another third in each case still evaluating what changes are needed.

**Agents are past the experiment stage.** 25% of developers reported using agentic AI regularly and a further 39% had experimented, for a combined 64%. Adoption concentrated on documentation (68%), automated test generation and execution (61%) and automated code review (57%), and perceived effectiveness tracked adoption closely, with documentation rated effective by 70%.

**Junior and senior developers diverge.** Developers with ten years' experience or less estimated 45% of their committed code was AI-assisted against 40% for those with over twenty years, reported a 40% average productivity increase against 32%, and reported higher job satisfaction (58% against 49%) and more time to advance their skills (62% against 51%) — while also being more likely to report that reviewing AI-generated code takes greater effort.

**Shadow adoption is uneven by tool.** Of the 74% of developers who had used ChatGPT in the past year, 52% accessed it through personal accounts, rising to 63% for Perplexity users; the report contrasts this with GitHub Copilot and Amazon Q Developer at 17% each and Cursor at 27%, which it reads as evidence of a more formal, top-down rollout for those tools.

## Context

This is a vendor report, and its figures should be read as such. The survey was Sonar's own, and its concluding chapter positions the company's SonarQube product as the answer to the bottleneck the report describes; at one point it reports that SonarQube users see stronger positive impacts on code quality, technical debt, rework costs, defects and vulnerabilities than non-users, a comparison drawn from its own customer base within its own survey. The report also states that its design was intended to build on findings in other leading developer surveys and answer questions the authors still had after reading them, so parts of it are framed as a response to work not reproduced here.

Methodologically, all respondents were 18 or older, employed full-time or self-employed in a technology role, write code or manage developers using at least one programming language, and had used AI as part of their job within the past year — so every figure describes AI users specifically, not developers in general. Sample sizes vary by question: most report n=1,149, while agentic-AI questions were asked of the 737 respondents using agents and technical-debt questions of 1,136.
