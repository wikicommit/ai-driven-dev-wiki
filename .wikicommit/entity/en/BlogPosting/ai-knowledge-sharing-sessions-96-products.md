---
title: "要件策定から本番環境への展開までの完全自動化を目指して96プロダクトのAI活用力を強化した話｜プロダクトのキーパーソン向け施策『AIナレッジ共有会』"
type: "schema:BlogPosting"
lang: en
tags: [ai-adoption, industry, engineering-organization]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/64511'
    hash: sha256:0fa964600209688a0e14a38c4200b5153352f2a460d1ad35da916bfad737e92f
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A CyberAgent post on the AI Knowledge Sharing Sessions, a programme in which key people from 96 products learned from teams already using AI, applied it in their own products and reported the results, and on the split between teams that advanced and teams that did not."
  author: ["kataoka"]
  publisher: "[[Organization/cyberagent]]"
---

This post, on the developers' blog of [[Organization/cyberagent]], is by a member of the company's corporate management division who has spent recent years on engineer-development programmes. It reports on the "AI Knowledge Sharing Sessions" (AIナレッジ共有会), a programme launched by the company's AI Driven Promotion Office — an organization set up in 2025 with the mission of supporting the careers of engineers who can thrive in the next AI era — to help teams, not just individuals, change how they develop with AI.

The post places the programme after two earlier steps: an annual investment of about ¥400 million in development AI agents, decided in June 2025, supporting about 1,200 engineers at US$200 per person per month; and generative-AI reskilling in three tiers, from a programme for over 6,200 employees of all job types to courses for 1,000 engineers. Those steps are said to have given individuals a common starting line, while best practices for AI-assisted development were not yet established and many teams were still feeling their way.

## Key Points

- The company's mid-term goal, announced internally in 2025, is to bring product-development teams to Level 4 of a five-level [[DefinedTerm/ai-maturity-levels]] scale by 2028, a state in which the development process from requirements through production deployment is fully automated.
- Rather than reach every engineer thinly, the sessions targeted people who could lead AI use in their teams, such as product tech leads nominated by their teams, on the idea that they would carry knowledge back and spread it.
- Each cycle had three steps: knowledge sharing, practice in the participant's own product, and an "output report" two months after the session that asks how much the knowledge was actually used, not how the session felt.
- Four sessions were held in six months, from October 2025 to April 2026 — a frequency the post says is needed because knowledge in this area goes stale quickly. Their themes moved from individual use to team use, a specific domain, and organizational change.
- Session 1 shared five-level definitions of AI use for individuals (from AI assistant to AI workflow development) and for teams (from code-level completion to an AI development team that builds features with almost no human intervention). One group company that adopted and regularly measured the individual levels saw the average score rise from 1.23 to 3.27 in six months.
- Session 2 was a hands-on of the core flow of AI-driven development as the company's AI Operations Office presented it: AI drafts a plan, a human reviews it, AI revises and executes it, and a human checks the result and gives feedback.
- Session 3 covered Unity development, which the post calls hard for AI agents because compiling, running the app and checking the screen are involved as well as editing code, including in-house Unity MCP work.
- Session 4 described a nine-step move to project-based AI-driven development, from breaking down the development flow through documentation, skills and semi-automatic execution to automatic pull-request review, together with a management change in which everyone acts as a project manager and delegates implementation to AI. The post highlights the observation that an environment easy for AI to work in is roughly one easy for newcomers to work in, since context written down for AI doubles as onboarding material.
- Over the six months key people from 96 products took part, across media and IP, advertising, games and headquarters functions.
- In the output reports for session 3, close to 90% of products chose one of the top two levels of use. Reported effects included about 30% less effort in requirements definition and development, about 75% less effort in specification and impact investigation, 1.5 to 2 times as many pull requests created, and 0.5 to 1 hour saved per code review. Participants also formed a community across business units and held an interim lightning-talk event of their own.
- The session-4 reports showed a split: just over 30% of products rated their use at 4 or above, while about 30% reported feeling no effect. The post's reading is that the sessions offered too little to teams already advanced and too high a bar for those behind, and that there is no quick universal fix.
- As next steps, the company is extending the regular measurement of individual AI-use levels company-wide, with the goal that every engineer reaches Level 3 — running several AIs in parallel and building workflows themselves — and has started an e-learning programme on AI-driven development for all engineers.

## Context

The post is written by the staff responsible for the programme and reports its own survey results; the effect figures are self-reported by participating products. It presents the programme as one of the company-wide measures towards the 2028 automation goal and is candid about the programme's uneven results.
