---
title: "Organizational adoption of AI coding agents"
lang: en
kind: practice
review_status: pending
generated_at: "2026-09-26"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"
derived_from:
  - path: .wikicommit/entity/en/BlogPosting/ai-knowledge-sharing-sessions-96-products.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce.md
    source_commit: 918f7af409eaecc35e50dea8e21fc3277faf15bf
  - path: .wikicommit/entity/en/BlogPosting/pj-double-mercari-development-productivity.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/BlogPosting/engineering-organization-reform-toward-full-development-automation-by-2028.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/Organization/zozo.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/Organization/cyberagent.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/Organization/zalando.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/Report/quantifying-github-copilots-impact-in-the-enterprise-with-accenture.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/BlogPosting/ai-driven-development-two-commands.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/Report/dora-ai-capabilities-model-2025.md
    source_commit: 8747b8ec3dcc7491d2de6b080020106d3f5da014
  - path: .wikicommit/entity/en/Organization/mercari.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/Organization/dmm.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/Organization/microsoft.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/BlogPosting/enabling-ai-usage-at-mercari-with-secure-devin-management.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/DefinedTerm/ai-mandate.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/ScholarlyArticle/ai-writes-faster-than-humans-can-review.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/BlogPosting/ai-code-agents-matsuri-seven-techniques.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/Event/ai-code-agents-matsuri-2025-winter.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/BlogPosting/agentic-engineering-at-zalando-a-snapshot.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/BlogPosting/raising-productivity-floor-with-harness.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/DefinedTerm/raising-the-floor.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/BlogPosting/choosing-ai-native-mercari-guiding-principles.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/BlogPosting/toss-ai-surf-day.md
    source_commit: f1038a285945837f7d6e6669210e65fb6f31011a
  - path: .wikicommit/entity/en/ScholarlyArticle/generative-ai-adoption-in-software-engineering.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/DefinedTerm/productivity-pressure-paradox.md
    source_commit: d2fb1a6ec03c16446d710a6305ae25342ee4b2b9
  - path: .wikicommit/entity/en/DefinedTerm/dora-ai-capabilities-model.md
    source_commit: 8747b8ec3dcc7491d2de6b080020106d3f5da014
---

This page sets side by side what this wiki records about organizations trying to make AI coding agents part of how a whole engineering organization works, rather than something a few individuals do well. The firsthand accounts come from [[Organization/cyberagent]], [[Organization/mercari]], [[Organization/zozo]], [[Organization/zalando]], [[Organization/github]], [[Organization/microsoft]], [[Organization/dmm]] and Toss. Around them sit studies and reports of other kinds: GitHub's study with Accenture, built around a randomized controlled trial; a telemetry study of Microsoft's own rollout; a longitudinal case study of one firm's "2×" [[DefinedTerm/ai-mandate]]; a practitioner questionnaire; and Google's survey-based [[DefinedTerm/dora-ai-capabilities-model]]. Most of the firsthand accounts are written by the organization about itself, which limits how far each can be taken. The last section sorts them by the kind of evidence behind them.

## The problem the accounts start from

Several accounts describe the same starting point, and it is not a lack of uptake. At ZOZO, development AI agents are provided to all engineers under a company-wide program. The difficulty is described as variance: engineers who used the tools well raised their productivity, but the knowledge stayed inside individual practice, so the organization's minimum level was slow to rise even as adoption spread. The same concern is stated at team level: assets each team built stayed inside it, which widened the gap between teams ([[Organization/zozo]]). The core-systems division's post describes prompts, review criteria and each person's sense of how much to delegate diverging from person to person, so that the ceiling rose while the floor stayed where it was ([[BlogPosting/ai-driven-development-two-commands]]).

Outside any one company's account, one engineer's post puts the same variance as a gap in know-how about controlling the tool, not in coding ability, and calls leaving it to individual aptitude a loss the organization bears. It names the response [[DefinedTerm/raising-the-floor]] ([[BlogPosting/raising-productivity-floor-with-harness]]).

Mercari's accounts tell the same story from several angles. In early 2025, AI tools and MCP servers were adopted bottom-up in what the company calls a "Divergence" phase. Some developers became dramatically more productive, a gap opened between those who could use AI well and those who could not, and shared practice stayed at the level of local tips and shared rule files ([[Organization/mercari]]). pj-double attributes this to the synchronous, interactive character of [[DefinedTerm/vibe-coding]]: the situational judgements stay inside each developer's chat logs ([[BlogPosting/pj-double-mercari-development-productivity]]). The CTO's post lists uneven prompt quality, difficulty gathering context, varying code quality and a spread of different tools. It traces all four to the absence of a shared regulation for how to use AI ([[BlogPosting/choosing-ai-native-mercari-guiding-principles]]).

Other accounts start from uneven reach rather than uneven results. At Toss, people in product, design and staff roles had been working out how to use AI in their own areas, but some team members still felt distant from it, and people in non-development roles grew anxious ([[BlogPosting/toss-ai-surf-day]]). CyberAgent's knowledge-sharing post describes company-wide investment and reskilling as having given individuals a common starting line, while many teams were still feeling their way ([[BlogPosting/ai-knowledge-sharing-sessions-96-products]]). A CyberAgent engineer describes the obstacle to spreading a tool in the first place: a company of more than 8,000 consolidated employees, separate Slack workspaces and independent technology choices per team, and a bottom-up culture in which a top-down "everyone uses this tool from tomorrow" rarely happens ([[BlogPosting/ai-code-agents-matsuri-seven-techniques]]).

Two sources frame the general case. GitHub's playbook says companies invest in AI tools only to see adoption confined to a small group of early enthusiasts. On its account they fail because they treat adoption as a technology problem when it is a change-management problem ([[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]). The practitioner questionnaire finds organizations far better at handing out tool access than at training, policy or objectives. Of respondents whose organization supports GenAI use, 81.06% report access to tools as a form of support, against 45.47% for training, 41.08% for published policies and 19.08% for objectives or KPIs tied to GenAI use ([[ScholarlyArticle/generative-ai-adoption-in-software-engineering]]).

## How adoption is reported to spread

Only one account measures how first use spreads. Microsoft's telemetry study found adoption of Copilot CLI to be substantially social. Engineers whose skip-level peers were largely using it had 216% higher odds of trying it. A direct manager's use was associated with 82% higher odds of trying it and 22% higher odds of sticking with it. Busier engineers were more likely both to try and to keep using it, while career stage and tenure mattered little. The authors state that the design cannot separate peer influence from homophily ([[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]]).

The other accounts describe deliberate channels for carrying practice between people. They differ in whom they target:

- **Volunteer advocates.** GitHub's playbook recruits AI advocates simply by asking for volunteers. They act as local experts, showcase use cases, feed their teams' views back and help co-lead training, supported through a "Train the Trainer" approach ([[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]).
- **Nominated evangelists.** Toss chose 142 evangelists by colleague nomination. The scheme selected the people most committed to spreading AI in their teams, not the most technically fluent, on the reasoning that using AI well for an organization means redesigning a team's workflow ([[BlogPosting/toss-ai-surf-day]]).
- **Key people per product.** CyberAgent's knowledge-sharing sessions targeted people who could lead AI use in their teams, such as nominated product tech leads, rather than reaching every engineer thinly. Key people from 96 products took part over six months ([[BlogPosting/ai-knowledge-sharing-sessions-96-products]]).
- **Attention from outside.** A member of CyberAgent's AI Driven Promotion Office, after internal talks and demos drew little response, organized an external event, [[Event/ai-code-agents-matsuri-2025-winter]]. The argument was that information from outside crosses internal organizational walls. By the time of writing, the post reports, the internal Cursor channel the author had started alone in September 2024 had over 500 members, and the company had about 1,000 active Cursor users across job types ([[BlogPosting/ai-code-agents-matsuri-seven-techniques]]).
- **Standing formats.** Zalando describes an LLM guild with weekly knowledge-sharing sessions, topic-driven hackathons, on-site GenAI Labs for around 20 people, and monthly trainings whose trainers are recruited from earlier Lab attendees ([[Organization/zalando]]). Toss set every Friday from April to June aside for experimenting with AI, with about 200 employee-run clubs created as the programme began ([[BlogPosting/toss-ai-surf-day]]). Microsoft ran an internal "Agentic Engineering Day" ([[Organization/microsoft]]). GitHub recommends distinct communities of practice, each with a charter and designated leaders, rather than one AI channel ([[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]).

## What the accounts do about it

### Tool choice: leaving it open or converging

The accounts differ most visibly on whether to standardize the tool itself. Zalando has never centrally mandated a single coding tool. With more than 200 teams exploring the ecosystem, it states that it is far too early to standardize and frames vendor independence as key ([[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]). One Mercari post describes the same stance, with everyone empowered to adopt tools of their choosing. It also reports the cost: the efficacy and output of those tools varied greatly, even within teams ([[Organization/mercari]]). The CTO's post describes the same divergence from the company level: Cursor was rolled out company-wide first, then engineers moved to newer assistants such as Claude Code, which made best practices hard to consolidate ([[BlogPosting/choosing-ai-native-mercari-guiding-principles]]). ZOZO's program covers a wide range of tools ([[Organization/zozo]]), and CyberAgent had introduced Claude Code and Codex on enterprise plans, with Cursor under consideration ([[BlogPosting/ai-code-agents-matsuri-seven-techniques]]).

Microsoft is the one account that moves toward a single tool. Its engineers had two sanctioned command-line agents in early 2026. Shortly after April 29, 2026, an internal announcement indicated that Claude Code licenses would be discontinued for most engineers, who were directed to Copilot CLI ([[Organization/microsoft]]). In its study, among single-tool users, weeks of Copilot CLI use showed a +24.9% lift in merged pull requests against +11.4% for Claude Code. The authors offer different task mixes and Microsoft's ownership of GitHub as hypotheses ([[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]]).

### A standard process rather than a standard tool

Where accounts standardize, several standardize the process and keep it independent of the tool. Mercari's pj-double worked with more than 30 backend projects for three months and, in September 2025, proposed [[DefinedTerm/agent-spec-driven-development]] (ASDD). The method was meant to institutionalize three practices the most effective developers shared: giving the AI primary information up front, stating purpose, steps and completion criteria, and keeping the AI's working context lean. From October the project extended to the whole company ([[BlogPosting/pj-double-mercari-development-productivity]]). The CTO's post describes ASDD as the core of the development process and stresses that its quality depends on the context supplied when writing the Agent Spec ([[BlogPosting/choosing-ai-native-mercari-guiding-principles]]).

ZOZO's core-systems division built two standard commands, `/dev-init` and `/dev-resume`, combining Claude Code and Codex. The user-facing surface is held at those two commands while the prompts, Skills, review criteria and integrations behind them are updated, so the organization can move to newer practice without engineers relearning an interface. The author argues against letting each team build its own workflow, which on the post's account raises local autonomy while leaving the organizational floor untouched ([[BlogPosting/ai-driven-development-two-commands]]). CyberAgent's sessions taught a core flow — AI drafts a plan, a human reviews it, AI revises and executes it, a human checks the result. Its fourth session described a nine-step move to project-based AI-driven development ([[BlogPosting/ai-knowledge-sharing-sessions-96-products]]).

### Shared assets between teams

Several accounts package working methods so that other teams can install them. ZOZO has operated a single [[DefinedTerm/claude-code-plugin-marketplace]] across teams since the second half of 2025. After roughly ten months it reports concrete reuse between teams and a shorter path for new members ([[Organization/zozo]]). Zalando maintains a centralized collection of [[DefinedTerm/agent-skills]] grouped into plugins, among which migration skills are a widely popular type ([[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]). At Mercari, isolating each team's Devin Organization made sharing know-how difficult, and making Devin Knowledge manageable through the in-house Terraform provider is what let it be distributed across teams ([[BlogPosting/enabling-ai-usage-at-mercari-with-secure-devin-management]]). The argument for this approach is made most fully in [[BlogPosting/raising-productivity-floor-with-harness]]. There a single slash command carries a strong engineer's whole workflow so that anyone runs it at the same quality, and plugin knowledge is layered into company-wide, domain and repository layers. The author offers this as a direction and mostly hypothesis, not a result.

### Policy, governance and platform

GitHub treats an acceptable-use policy, developed with IT, HR, Security and Legal, as a prerequisite. It recommends a tiered model in which a tool not on the vetted list is treated as public ([[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]). DORA recommends a risk-based policy from a cross-functional working group. The policy sorts uses into prohibited, permitted with guardrails, and allowed, and is published as a living document ([[Report/dora-ai-capabilities-model-2025]]). Zalando handles governance through existing mechanisms: an AI section added to its Tech Radar, and auto-detection of AI model usage by scanning deployed Docker images ([[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]).

Two accounts describe the platform work that organization-wide rollout required. Zalando's ML platform team deployed a [[SoftwareApplication/litellm]]-based proxy in January 2024, which gave the platform team a single point at which to measure adoption ([[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]). Mercari's AI Security team built a Terraform provider and automation for Devin across more than ten Organizations. It covers member and permission management, per-team usage caps, bulk secret rotation, API key expiry and audit logs, most of it because a standard feature did not exist ([[BlogPosting/enabling-ai-usage-at-mercari-with-secure-devin-management]]). DORA's finding on platforms is that when internal platform quality is low, AI adoption's effect on organizational performance is negligible; when it is high, the effect becomes strong and positive ([[Report/dora-ai-capabilities-model-2025]]).

### Mandates and targets

Several accounts attach a numeric goal. CyberAgent's management adopted the aim of fully automating its development process, equated with AI maturity Level 4, by 2028 ([[BlogPosting/engineering-organization-reform-toward-full-development-automation-by-2028]]). Mercari's Double project is named for its aim of doubling productivity ([[BlogPosting/pj-double-mercari-development-productivity]]). The firm in the mandate case study set a goal, in a CTO memo, of doubling engineering productivity over twelve months, with merged pull requests per engineer per month as the measure ([[ScholarlyArticle/ai-writes-faster-than-humans-can-review]]).

[[DefinedTerm/ai-mandate]] records the range such commitments span: from Shopify making effective AI use "a fundamental expectation" of every employee to Coinbase dismissing engineers who did not adopt. The case study finds the mandate itself leaves only a small residual in the throughput gain, most of which it attributes to adoption and to a return that grows with accumulated use. The authors therefore call the mandate catalytic rather than directly productive, and describe it as "a process-redesign problem, not a tooling deployment". [[DefinedTerm/productivity-pressure-paradox]] names the failure the paper associates with demanding the target before the skill accrues. The paper also warns that a broadcast target invites measurement inflation its own design cannot fully separate from genuine acceleration.

GitHub's playbook describes a different lever from a target: leaders explain the "why" in terms of daily work and are transparent that AI will change jobs ([[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]). DORA lists a clear and communicated AI stance as one of its seven capabilities ([[DefinedTerm/dora-ai-capabilities-model]]).

### Roles, careers and skills

CyberAgent is the account that goes furthest into careers. Its executive's post groups engineers' reactions to the 2028 vision into five anxieties — careers, skill deterioration, unfair evaluation, a shift in engineers' value, and inequality between teams — and attaches a measure to each. The measures are a renewed evaluation system built around four career ladders, stronger training for junior engineers, an engineer-specific AI ranking, and the AI Driven Promotion Office ([[BlogPosting/engineering-organization-reform-toward-full-development-automation-by-2028]]). GitHub gives senior individual contributors a dual mandate: to use AI in their own work and to scale AI fluency to others ([[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]).

Two accounts reach past engineering. Mercari's AI Task Force divided the company into 33 domains, grew to about 100 members and inventoried about 4,000 workflows. Its stated reasoning is that faster coding alone cannot speed up releases if legal, security and compliance checks still wait on people ([[BlogPosting/choosing-ai-native-mercari-guiding-principles]]). Toss's programme was framed from the outset around the gap felt in non-development roles, and its OpenAI collaboration day held hands-on sessions for non-developers alongside developers ([[BlogPosting/toss-ai-surf-day]]).

On skill-building, Zalando reports that participants are strongly tempted to use coding agents as a shortcut in sessions meant to build skills, which usually inhibits learning ([[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]). The questionnaire's most common barrier among non-users was lack of required skills or time constraints ([[ScholarlyArticle/generative-ai-adoption-in-software-engineering]]).

## How the accounts measure it

The accounts measure different things, and several separate adoption from impact:

- **Adoption breadth and depth.** GitHub's playbook measures in three phases: breadth (monthly active and engaged users), depth (segmenting users by days active per month), then business impact ([[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]). The Accenture study reports 81.4% of developers installing the extension on the day they received a license ([[Report/quantifying-github-copilots-impact-in-the-enterprise-with-accenture]]).
- **Organizational readiness.** ZOZO's All ZOZO AI Readiness Score (AZARS) looks at how far an individual has built AI into their work and at whether the organization has encoded AI-premised processes into systems ([[Organization/zozo]]). CyberAgent uses five-level definitions of AI use. One group company that measured them saw the average rise from 1.23 to 3.27 in six months, and the company is extending the measurement company-wide ([[BlogPosting/ai-knowledge-sharing-sessions-96-products]]).
- **Use two months later.** CyberAgent's sessions end in an "output report" two months later that asks how much the knowledge was actually used, not how the session felt ([[BlogPosting/ai-knowledge-sharing-sessions-96-products]]).
- **Throughput.** The Accenture RCT reports an 8.69% increase in pull requests and an 84% increase in successful builds ([[Report/quantifying-github-copilots-impact-in-the-enterprise-with-accenture]]). Microsoft estimates a +24.0% lift in merged pull requests for early adopters ([[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]]). The mandate study reports pull requests per active developer rising 2.09× ([[ScholarlyArticle/ai-writes-faster-than-humans-can-review]]). Mercari compared each project's effort estimate with its actual effort, and reports more than a 150% improvement for projects using spec-driven development ([[BlogPosting/pj-double-mercari-development-productivity]]).
- **Quality guards.** Mercari monitors revert rate and MTTR with the DX tool ([[BlogPosting/pj-double-mercari-development-productivity]]). Zalando tracks pull-request size distributions and cyclomatic complexity in four codebases ([[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]). GitHub's playbook notes that AI can lead to larger pull requests, which makes pull-request size worth watching ([[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]]).

Several sources say plainly what their chosen measure misses. The Microsoft authors call merged pull requests an imperfect proxy that rewards small, frequent PRs and may miss quality costs ([[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]]). The mandate study argues that velocity-centric frameworks register the authoring speedup but miss where the displaced work went ([[ScholarlyArticle/ai-writes-faster-than-humans-can-review]]). In the questionnaire, 58.15% of respondents use no objective metric for size, productivity or quality, and the authors treat the reported gains as perceptions ([[ScholarlyArticle/generative-ai-adoption-in-software-engineering]]).

## Where the accounts report it falling short

**Uneven results after a programme.** CyberAgent's session-4 reports show just over 30% of products rating their use at 4 or above, while about 30% reported no effect. The post's reading is that the sessions offered too little to teams already advanced and too high a bar for those behind ([[BlogPosting/ai-knowledge-sharing-sessions-96-products]]).

**The review stage.** In the mandate study, pull-request volume grew 3.1× while the pool of reviewers grew only 1.5×. The share of pull requests receiving a human review fell from 89% to 68% as automated AI review rose to about 84%, and human review thinned toward bare approval ([[ScholarlyArticle/ai-writes-faster-than-humans-can-review]]). DMM reports that as AI-agent adoption advanced across the company in 2025, the load of code review rose sharply ([[Organization/dmm]]). Mercari's pj-double located its review strain in pull-request size rather than in the code being AI-written, and reports removing it by splitting work into one PR per task ([[BlogPosting/pj-double-mercari-development-productivity]]). Zalando reports growth in large pull requests and teams that get carried away with PRs that discourage reviewers, and describes a risk-based approval bot that auto-approves the 33% of PRs it classifies as low risk ([[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]). See [[DefinedTerm/review-bottleneck]] for this wiki's page on the pattern.

**Where gains do not reach.** The mandate study finds the gain concentrated in newer repositories and not significant in legacy ones ([[ScholarlyArticle/ai-writes-faster-than-humans-can-review]]). Zalando notes that many reported throughput gains come from monorepos, whereas it largely uses separate repositories for microservices ([[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]). Mercari's CTO states that the company does not yet regard itself as AI-Native despite 95% of employees using AI tools, because coding productivity alone does not raise the productivity of the whole organization ([[BlogPosting/choosing-ai-native-mercari-guiding-principles]]).

**Limits of the standard process.** pj-double reports that the Agent Spec assumes a specification and design already agreed, when reaching agreement was what took longest. The team's own diagnosis is that it treated work that should be done by thinking and deciding together with AI as work to be delegated to AI ([[BlogPosting/pj-double-mercari-development-productivity]]). It also describes an early internal QA tool with a rich UI as a "build trap" that made the method harder to improve. ZOZO's two-command post reports that effect measurement is still outstanding ([[BlogPosting/ai-driven-development-two-commands]]).

**Sharing between parallel efforts.** Mercari's AI Task Force reports that running 33 domains independently made decisions fast but left best practices and retrospectives poorly shared between them ([[BlogPosting/choosing-ai-native-mercari-guiding-principles]]). The company's own posts describe tool freedom, per-team isolation and a company-wide process standard without reconciling them ([[Organization/mercari]]).

**Amplifying what is already there.** DORA's central claim is that AI magnifies the strengths of high-performing organizations and the dysfunctions of struggling ones. With low user-centricity, AI adoption is associated with decreased team performance ([[Report/dora-ai-capabilities-model-2025]]). Zalando's closing theme is the same: AI amplifies both good and bad existing practice ([[BlogPosting/agentic-engineering-at-zalando-a-snapshot]]). In Microsoft's study, prior IDE Copilot use raised the odds of trying the new CLI tool but was associated with lower retention. The authors interpret this as engineers having a familiar fallback ([[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]]).

## What kind of evidence stands behind each account

| Account | Who writes it | Kind of evidence |
|---|---|---|
| [[BlogPosting/engineering-organization-reform-toward-full-development-automation-by-2028]] | CyberAgent's executive in charge of technology | Statement of policy and intent; describes measures, not effects |
| [[BlogPosting/ai-knowledge-sharing-sessions-96-products]] | Staff running the programme at CyberAgent | Programme report; effect figures self-reported by participating products |
| [[BlogPosting/ai-code-agents-matsuri-seven-techniques]] | The CyberAgent engineer who ran the effort | First-person account; the author's own figures; techniques are experience, not a tested method |
| [[BlogPosting/pj-double-mercari-development-productivity]] | A manager in Merpay's VPoE office | Internal measurements; productivity figures rest on subjective estimate-versus-actual comparisons |
| [[BlogPosting/choosing-ai-native-mercari-guiding-principles]] | Mercari's CTO | Statement of direction; the company's own figures |
| [[BlogPosting/enabling-ai-usage-at-mercari-with-secure-devin-management]] | A Mercari AI Security engineer | Operator's account of tooling built; no outcome measurement |
| [[BlogPosting/ai-driven-development-two-commands]] | Written from one ZOZO division | One division's deployment; effect measurement outstanding |
| [[BlogPosting/agentic-engineering-at-zalando-a-snapshot]] | A Zalando Executive Principal Engineer | Company's analysis of its own repositories; behaviour change explicitly anecdotal |
| [[BlogPosting/toss-ai-surf-day]] | Toss's Developer Relations Manager | Firsthand account; participant quotations rather than measured outcomes |
| [[Organization/dmm]] | One DMM group, on its own blog | How that group describes its organization |
| [[BlogPosting/raising-productivity-floor-with-harness]] | One engineer | Argument offered as direction and mostly hypothesis |
| [[TechArticle/githubs-internal-playbook-for-building-an-ai-powered-workforce]] | The program manager director of GitHub's internal "AI for Everyone" initiative | GitHub's account of its own program; no outcome figures |
| [[Report/quantifying-github-copilots-impact-in-the-enterprise-with-accenture]] | GitHub with Accenture and Microsoft researchers | Randomized controlled trial, adoption analysis and user survey; run and published by the product's vendor |
| [[ScholarlyArticle/adoption-and-impact-of-command-line-ai-coding-agents]] | Microsoft researchers | Developer-level telemetry, synthetic control and fixed effects; one company, one window, authors disclose proximity to a tool seller |
| [[ScholarlyArticle/ai-writes-faster-than-humans-can-review]] | Carnegie Mellon and Stanford researchers | Longitudinal panel of one firm; rollout not randomized; the site is described as near-ideal, so an upper envelope |
| [[ScholarlyArticle/generative-ai-adoption-in-software-engineering]] | Academic researchers | Questionnaire of 204 practitioners; non-probabilistic sample; benefits are perceptions |
| [[Report/dora-ai-capabilities-model-2025]] | Google's DORA programme | Survey of nearly 5,000 professionals plus qualitative data; its inaugural model |

Of the three studies that measure outcomes, the Accenture RCT and Microsoft's telemetry study are each run by or close to a company that sells the tool measured. The independent academic case study is of a single firm, which its authors describe as near-ideal rather than representative. The firsthand accounts carry most of the detail about the organizational measures themselves, and almost all of them report the company's own figures or none.
