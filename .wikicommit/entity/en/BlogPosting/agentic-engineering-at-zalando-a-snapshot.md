---
title: "Agentic Engineering at Zalando: a snapshot"
type: "schema:BlogPosting"
lang: en
tags: [agentic-engineering, enterprise-adoption, developer-platform, governance]
sources:
  - type: url
    url: 'https://engineering.zalando.com/posts/2026/08/agentic-engineering-at-zalando-a-snapshot.html'
    hash: sha256:33171882bb4809ae93923b09f4e1fe6315bf6de5690393243df5a995118678bc
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A firsthand account, written by an Executive Principal Engineer at Zalando, of two and a half years of agentic engineering practice across more than 250 engineering teams — covering the LLM proxy the platform was built on, what the company observed in its own pull-request and code-complexity data, a risk-based PR approval bot, and the governance and knowledge-sharing formats it settled on."
  author: "Bartosz Ocytko"
  datePublished: "2026-08-14"
  publisher: "[[Organization/zalando]]"
---

This post is an organization-scale retrospective rather than an argument about what agentic
engineering ought to be. Written by Bartosz Ocytko, an Executive Principal Engineer at Zalando,
it looks back over what the company describes as two and a half years of work across more than
250 engineering teams and sets out the approaches it says worked. Its framing is that the
industry as a whole is still figuring out how to approach agentic engineering, and that value
and impact from large language models are arriving in different forms and at different paces
across the company's business lines.

What distinguishes the account from vendor material on the same subject is that most of its
claims are about Zalando's own measurements and its own operational choices: how many pods the
LLM proxy runs on, what fraction of pull requests an approval bot auto-approves, what happened
to code complexity in four named codebases once coding agents entered them. The post is
explicit that it is a snapshot of an evolving practice and ends by inviting other non-vendor
engineering teams working on similar problems to get in touch.

The organizing decision it describes is a deliberate refusal to converge. With more than 200
teams exploring the ecosystem, the post states the company's position that it is far too early
to standardize on one tool, and that its objective instead is transparency and exchange between
teams.

## Key Points

- Zalando's ML platform team deployed a [[SoftwareApplication/litellm]]-based API proxy in
  January 2024 to give engineers API-based access to models from multiple providers, giving the
  platform team a single point at which to measure adoption.
- The company has never centrally mandated a single coding tool; users choose based on available
  models and their own preference for IDE or CLI, and the post frames vendor independence as key
  in a fast-moving environment.
- Users become attached to the coding agent they have been using despite what the post describes
  as rather low switching costs, since the tools' capabilities are largely similar — the author
  presents this hesitance as psychological rather than technical.
- Zalando reports seeing the impact of AI coding in its pull-request data for two years: a
  consistent increase in PRs of 100–500 changed lines, plus growth in the 500–1,000 and
  1,000–2,000 buckets since the Sonnet 4 release in Q2 2025.
- Mapping commit-level code quality metrics across four Java and Go codebases, the company says
  it can pinpoint inflection points in total cyclomatic complexity at the time coding agents
  entered each codebase; in codebases that used agents fully from the start, complexity builds up
  very quickly and then fades out. This is the company's own analysis of its own repositories.
- Commit messages themselves carry a footprint of coding agents, typically around the 5,000
  character mark — in one case a commit message included a full unit test execution log.
- A risk-based PR approval bot classifies each PR as low, medium or high rollout risk at creation
  time; the post reports that 33% of PRs are low-risk and auto-approved, which it says reduced PR
  lead time by 20–40% compared with all PRs. Its rule set was built from analysis of the
  company's own production incidents and is described as highly specific to its tech stack.
- The post reports anecdotal evidence that the approval bot changed engineers' behaviour: PRs
  began to be split so that backwards-compatible changes ship quickly as low risk, where
  previously such changes were mixed with riskier ones.
- Zalando maintains a centralized collection of [[DefinedTerm/agent-skills]] grouped into
  plugins, addressing common tasks across disciplines and languages; the post says migration
  skills — guiding teams through adopting new platform tools or infrastructure practices — are a
  widely popular type.
- Session data from coding agents is described as highly educational, both for spotting
  non-essential traffic that costs tokens (generating plan names, terminal window titles, recaps
  for idle sessions) and for letting users learn about their own prompting patterns.
- Governance is handled through existing mechanisms rather than new ones: an AI section was added
  to the company's Tech Radar, and AI model usage is auto-detected by scanning deployed Docker
  images, after which owners are asked for documentation or a legal review.
- On training, the post states that participants are strongly tempted to use coding agents as a
  shortcut in sessions meant to build skills, and that doing so usually inhibits learning — so
  trainers are advised to state explicitly when manual coding is expected.

## Context

The post positions itself against accounts from vendors and from monorepo-heavy organizations.
It notes that many reported AI wins and increases in PR throughput across the industry come from
monorepos where leverage is high, whereas Zalando largely uses separate repositories for its
microservices — which is the stated reason it plans a scanner to assess each repository's AI
readiness.

Its caveats are mostly about the limits of its own evidence. The complexity analysis relies on
commits carrying `Co-authored-by` markers to confirm inflection points, and the author notes that
open-source codebases are less consistent in this because not all authors disclose coding agent
use. On the risk-based approval bot's effect on behaviour, the post says explicitly that the
evidence is anecdotal. The prediction that complexity plateauing for a well-scoped microservice
means build time has been drastically reduced is stated as a hope, with the author writing that
time will show whether this is the case.

The closing theme is that AI amplifies both good and bad existing practice rather than changing
it in one direction: teams that get carried away end up with large PRs that discourage reviewers
and slow delivery until the team adjusts, while investments in platform capabilities — such as
the web monorepo's per-PR deployment wired to live data — pay off by letting non-engineers
prompt changes and review results before handing over to engineers.
