---
title: "Organizational adoption of AI coding agents"
lang: en
kind: practice
review_status: pending
generated_at: "2026-09-26"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
derived_from:
  - path: .wikicommit/entity/en/BlogPosting/ai-knowledge-sharing-sessions-96-products.md
    source_commit: ec1aed6cc815a0de19917c1c3fa9646b24090b11
  - path: .wikicommit/entity/en/TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce.md
    source_commit: 918f7af409eaecc35e50dea8e21fc3277faf15bf
  - path: .wikicommit/entity/en/BlogPosting/pj-double-mercari-development-productivity.md
    source_commit: ec1aed6cc815a0de19917c1c3fa9646b24090b11
  - path: .wikicommit/entity/en/BlogPosting/engineering-organization-reform-toward-full-development-automation-by-2028.md
    source_commit: ec1aed6cc815a0de19917c1c3fa9646b24090b11
  - path: .wikicommit/entity/en/Organization/zozo.md
    source_commit: ec1aed6cc815a0de19917c1c3fa9646b24090b11
  - path: .wikicommit/entity/en/Organization/cyberagent.md
    source_commit: ec1aed6cc815a0de19917c1c3fa9646b24090b11
  - path: .wikicommit/entity/en/Organization/zalando.md
    source_commit: ec1aed6cc815a0de19917c1c3fa9646b24090b11
  - path: .wikicommit/entity/en/Report/quantifying-github-copilots-impact-in-the-enterprise-with-accenture.md
    source_commit: fc6f8839ef49b4ad99a056d9f2d3011a9e22d960
  - path: .wikicommit/entity/en/BlogPosting/ai-driven-development-two-commands.md
    source_commit: ec1aed6cc815a0de19917c1c3fa9646b24090b11
  - path: .wikicommit/entity/en/Report/dora-ai-capabilities-model-2025.md
    source_commit: 8747b8ec3dcc7491d2de6b080020106d3f5da014
---

This page sets side by side the accounts in this wiki of organizations trying to make AI coding agents part of how a whole engineering organization works, rather than something a few individuals do well. The accounts come from [[Organization/cyberagent]], [[Organization/mercari]], [[Organization/zozo]], [[Organization/zalando]] and [[Organization/github]], with two reports alongside them — GitHub's study with Accenture, built around a randomized controlled trial, and Google's survey-based DORA report. Almost all of them are written by the organization about itself, which matters for how far each can be taken; the last section sorts them by the kind of evidence behind them.

## The problem the accounts start from

Several of the accounts describe the same starting point, and it is not a lack of uptake. At ZOZO, development AI agents are provided to all engineers under a company-wide program, and the difficulty is described as variance: engineers who used the tools well raised their productivity, while the knowledge stayed inside individual practice, so the organization's minimum level was slow to rise even as adoption spread ([[Organization/zozo]]). The core-systems division's post puts it as prompts, review criteria and sense of how much to delegate having diverged from person to person, so that the ceiling rose while the floor stayed where it was ([[BlogPosting/ai-driven-development-two-commands]]).

Mercari's pj-double tells the same story: individual developers achieved large gains in the first wave of AI-assisted coding, but the methods stayed personal and did not add up to an organizational improvement. It attributes this to the synchronous, interactive character of [[DefinedTerm/vibe-coding]], whose situational judgements stay inside each developer's chat logs ([[BlogPosting/pj-double-mercari-development-productivity]]). CyberAgent's knowledge-sharing post describes an organization in which company-wide investment and reskilling had given individuals a common starting line, while many teams were still feeling their way ([[BlogPosting/ai-knowledge-sharing-sessions-96-products]]).

GitHub's playbook frames the general case: companies invest in AI tools only to see adoption confined to a small group of early enthusiasts, and they fail because they treat adoption as a technology problem when it is a change-management problem ([[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]).

## What the accounts do about it

### A standard workflow

Two accounts respond by encoding a way of working. ZOZO's core-systems division collapsed its process into two standard commands, `/dev-init` and `/dev-resume`, holding the user-facing surface fixed while the prompts, Skills and integrations behind it are updated, and taking an explicit position against letting each team build its own workflow, which the author argues leaves the organizational floor untouched ([[BlogPosting/ai-driven-development-two-commands]]). Mercari's pj-double studied more than 30 backend projects for three months and then proposed [[DefinedTerm/agent-spec-driven-development]] (ASDD) as a standard, to institutionalise the practices of the developers who got the most from AI ([[BlogPosting/pj-double-mercari-development-productivity]]).

The two differ in what they assume. The ZOZO commands decide what to delegate from the direction of information transformation and keep abstract-to-concrete work — shaping requirements, choosing between options, prioritizing — with people. ASDD, by what Mercari's developers later reported, assumed a specification and design that were already agreed, when reaching agreement was what took longest.

### Shared assets between teams

ZOZO also runs a single [[DefinedTerm/claude-code-plugin-marketplace]] across teams, in response to the concern that each team's skills and agents stayed inside the team that made them; after roughly ten months it reports reuse between teams and a shorter path for new members ([[Organization/zozo]]). Zalando describes a centralized collection of [[DefinedTerm/agent-skills]] distributed as plugins ([[Organization/zalando]]).

### People who carry the practice

Several accounts route adoption through selected people rather than through everyone at once. CyberAgent's AI Knowledge Sharing Sessions targeted people who could lead AI use in their teams, such as nominated product tech leads, over four sessions in six months, each followed by a report on how much of the knowledge was actually used ([[BlogPosting/ai-knowledge-sharing-sessions-96-products]]). GitHub's playbook puts a volunteer network of AI advocates and distinct communities of practice among its eight pillars, alongside a dedicated responsible individual described as an enabler rather than a gatekeeper ([[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]). Zalando describes an LLM guild with weekly knowledge-sharing sessions, hackathons, GenAI Labs sessions and monthly trainings whose trainers are recruited from earlier Lab attendees ([[Organization/zalando]]).

### Policy and platform

GitHub's playbook treats an acceptable-use policy as a prerequisite, with a tiered model separating vetted tools from public ones. DORA's report recommends a clear AI stance produced by a cross-functional working group, sorting uses into prohibited, permitted with guardrails, and allowed ([[Report/dora-ai-capabilities-model-2025]]). On the platform side, Zalando's ML platform team runs an internally hosted [[SoftwareApplication/litellm]]-based proxy giving access to models from several providers ([[Organization/zalando]]). DORA reports that when internal platform quality is low, AI adoption's effect on organizational performance is negligible, and that when it is high the effect becomes strong and positive.

### Evaluation and careers

CyberAgent is the account that ties adoption to the evaluation system. Its executive in charge of technology set out an aim of fully automating the development process by 2028, and attached measures to five anxieties engineers raised: a renewal of the JB Career Program around four career ladders, stronger training for junior engineers, an engineer-specific AI ranking evaluating on engineering quality and technical maturity, and an AI Driven Promotion Office to address inequality between teams ([[BlogPosting/engineering-organization-reform-toward-full-development-automation-by-2028]]). This post describes measures announced or under way, not their effects.

## How the accounts measure it

The accounts measure different things:

- **Readiness of individuals and the organization.** ZOZO's All ZOZO AI Readiness Score (AZARS) looks both at how far an individual has built AI into their work and at whether the organization has encoded AI-premised processes into systems ([[Organization/zozo]]).
- **Levels of use.** CyberAgent's sessions shared five-level definitions of individual AI use; one group company that adopted and regularly measured them saw the average score rise from 1.23 to 3.27 in six months, and the company is now extending that measurement company-wide ([[BlogPosting/ai-knowledge-sharing-sessions-96-products]]).
- **Breadth, depth and impact.** GitHub's playbook measures in three phases — breadth of adoption, depth of engagement, and business impact — and notes that AI can lead to larger pull requests, which is why pull-request size is worth watching ([[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]).
- **Estimate against actual effort.** pj-double compared each project's conventional effort estimate with its actual effort, statistics the post itself calls subjective ([[BlogPosting/pj-double-mercari-development-productivity]]).
- **A controlled trial.** The Accenture study randomly assigned developers to groups with and without [[SoftwareApplication/github-copilot]] and collected DevOps telemetry, alongside an adoption analysis and a survey ([[Report/quantifying-github-copilots-impact-in-the-enterprise-with-accenture]]).

## Where the accounts report it falling short

The accounts record their own limits:

- **Uneven results.** CyberAgent's session-4 reports showed just over 30% of products rating their use at 4 or above, and about 30% reporting no felt effect. The post's reading is that the sessions offered too little to advanced teams and too high a bar to those behind, and that there is no quick universal fix.
- **A standard that assumed too much.** Mercari's developers reported that ASDD assumed an agreed specification and design. Auto-generated documents carried no rationale, and reviewing a regenerated Agent Spec cost more than writing one by hand. The team's diagnosis is that it treated work that should be done by thinking and deciding together with AI as work to delegate to it. The same post calls its first QA tool a "build trap", because the app made the method harder to change.
- **Costs and effects not yet measured.** ZOZO's two-command post reports that the Codex pairing costs more time and money than Claude Code alone. It also says effect measurement is still outstanding.
- **No silver bullet.** GitHub's playbook concludes that adoption takes sustained effort and that tools without an enablement strategy waste resources.
- **Weak foundations.** DORA's central claim is that AI amplifies an organization's existing strengths and dysfunctions. With low user-centricity, AI adoption is associated with decreased team performance.

On review load, pj-double concludes that strain came from pull-request size rather than from AI authorship, and that splitting work into small units removed it ([[DefinedTerm/review-bottleneck]]). DORA's report finds that working in small batches amplifies AI's effect on product performance, while slightly reducing the individual-effectiveness gains teams perceive from AI.

## What kind of evidence stands behind each account

| Account | Who wrote it | What it rests on |
|---|---|---|
| [[BlogPosting/ai-knowledge-sharing-sessions-96-products]] | The staff running the programme | Self-reported output reports from participating products |
| [[BlogPosting/engineering-organization-reform-toward-full-development-automation-by-2028]] | CyberAgent's own management | A statement of policy and intent, not results |
| [[BlogPosting/pj-double-mercari-development-productivity]] | A manager in Merpay's VPoE office, where the project was launched | Internal measurements; productivity from subjective estimate-versus-actual comparisons |
| [[BlogPosting/ai-driven-development-two-commands]] and [[Organization/zozo]] | ZOZO's own engineers | One division's deployment, whose effects are not yet measured, and one cross-team marketplace reporting reuse after about ten months |
| [[Organization/zalando]] | Zalando's own published account | A firsthand snapshot of the company's platform and practices |
| [[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]] | GitHub, about its own programme | An operating model; states no outcome figures |
| [[Report/quantifying-github-copilots-impact-in-the-enterprise-with-accenture]] | GitHub, with Accenture | A randomized controlled trial, adoption analysis and survey, by the vendor of the product measured |
| [[Report/dora-ai-capabilities-model-2025]] | Google's DORA programme | Survey responses from nearly 5,000 professionals and over 100 hours of qualitative data |

Only the last two draw on data collected beyond a single organization's account of itself, and one of those was conducted by the vendor of the product it measures.
