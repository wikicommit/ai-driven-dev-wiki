---
title: "Devin"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, coding-tools, agent-security, agentic-code-review]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2509.06216'
    hash: sha256:e5099cc3ed705ea5b891ef76e6da268494f7bb38bede48a7d37ea2f1b0888e66
  - type: url
    url: 'https://engineering.mercari.com/en/blog/entry/20260403-secure-devin-management/'
    hash: sha256:bc915a8ef4d5b712d51f417e33760f31692d9d15436252e3de284e4235644d53
  - type: url
    url: 'https://tech-blog.yayoi-kk.co.jp/entry/2026/02/18/110000'
    hash: sha256:f257dca18ea047972a127fe941a248ac2184ccbbb5bd4fc88d619fb52132227a
  - type: url
    url: 'https://cognition.com/blog/devin-annual-performance-review-2025'
    hash: sha256:9faf159b1a9fcb52db11ab77a27cff8fad27e55cef689d325eedb664358b64ea
  - type: url
    url: 'https://cognition.com/blog/introducing-devin'
    hash: sha256:73d2b8bef9a54736f9a6e7d6f3a7897727764c71d604e77c4ab4b9643a59d302
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "Cognition's autonomous coding agent, cited as an emerging example of goal-agentic (Level 3, SE3.0) AI software engineering that can take a well-defined technical goal and execute a multi-step plan across code, documentation, and other project artifacts. An enterprise operator's account describes it as a service that can autonomously investigate code, write code, and submit pull requests; a separate practitioner account describes driving it as a pull-request reviewer through its session API. Cognition's own 2025 review of the agent describes it as strongest on clearly scoped, verifiable tasks run in parallel and on understanding large codebases, and weakest on ambiguous or changing requirements."
  applicationCategory: "Autonomous coding agent"
  author: "[[Organization/cognition]]"
---

Devin is [[Organization/cognition]]'s autonomous coding agent, announced by Cognition in March 2024 as "the first AI software engineer" ([[BlogPosting/introducing-devin]]). It is discussed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] alongside Google's [[SoftwareApplication/google-jules]], OpenAI's Codex, and Anthropic's [[SoftwareApplication/claude-code]] as an example of an agent aiming for Goal-Agentic (Level 3, SE3.0) capability in the paper's [[DefinedTerm/se-autonomy-levels]] hierarchy: taking a well-defined technical goal (e.g. "add a caching layer") and executing a multi-step plan, self-devised or human-guided, across code, documentation, and other essential project artifacts.

A team operating it at Mercari describes it in more workaday terms, as a service that can autonomously investigate code, write code and submit pull requests, and notes that operating it at an organizational level comes with several management challenges ([[BlogPosting/enabling-ai-usage-at-mercari-with-secure-devin-management]]). A team at Yayoi describes using it as a pull-request reviewer, one of several uses it reports for the agent ([[BlogPosting/ai-code-review-ideal-and-reality]]).

## Capabilities

Cognition's launch post describes the agent's working environment: Devin is equipped with a shell, a code editor and a browser inside a sandboxed compute environment, and Cognition attributes its ability to plan and execute complex engineering tasks requiring thousands of decisions to advances in long-term reasoning and planning. The same post stresses collaboration alongside autonomy — Devin reports its progress in real time, accepts feedback, and works through design choices with the user as needed — and describes it as able either to build alongside an engineer or to complete tasks independently for the engineer to review. At launch it was available only in early access, through a waitlist.

The paper cites [[SoftwareApplication/deepwiki]], used by Devin, as an early example of a persistent-memory capability: it lets the agent build and refer to its own documentation and decision logs across multiple tasks, creating continuity and helping prevent it from repeating past mistakes — an example the paper uses to motivate its proposed [[DefinedTerm/ai-teammate-lifecycle-engineering]] activity.

The Mercari account describes the execution model an operator has to work with: Devin launches an independent virtual machine for each session, so in its initial state it holds permissions only for source-code management services such as GitHub, and connecting it to cloud environments or ticket-management services means configuring credentials such as API keys individually. That post also records that members within an Organization can access the file system and shell inside sessions, and that as an AI agent Devin can freely use any API key it is given — two properties it treats as the reason credentials must be handled with care.

Several product surfaces appear in that account. Devin Knowledge is described as functioning similarly to Agent Skills within Devin. Devin MCP is the interface through which agents reach Devin, and requires an API key. Devin Wiki allows retrieval of repository contents and natural-language search through Devin MCP; the post's stated reason for delegating source-code investigation to it is that an AI agent exploring source code directly consumes a large amount of context, which delegating reduces.

The Yayoi account adds two behaviors relevant to unattended use. It reports that Devin refers to [[DefinedTerm/agents-md]] automatically, and gives that as the reason recording project-specific rules and context there yields more accurate review; that team keeps setup commands, code style and test guidelines, project structure and workflow notes in it. It also describes review sessions being created programmatically — an authenticated POST against the Devin API's sessions endpoint, carrying a prompt assembled by the caller — with Devin posting its findings back as comments on the pull request. That team reports session start-up being slow at first and improving on two counts it states separately — the agent learning the project over time, and project information being defined in advance in the review prompt and in AGENTS.md — while first sessions stayed slow; that is one team's observation rather than a published characteristic.

The Yayoi post also notes a newer feature called Devin Review — described there as a comprehensive code review platform offered as a web application, with diff organization and bug-catching capabilities. That team had not compared it against the API-driven approach at the time of writing.

### The vendor's own assessment

Cognition's [[BlogPosting/devins-2025-performance-review]], published eighteen months after launch, is the vendor's account of where the agent performs well and where it does not, framed as a performance review of an engineer. It reports that calibrating Devin against a traditional engineering competency matrix was difficult, because Devin is senior-level at codebase understanding but junior at execution.

On execution, Cognition says Devin does best on tasks with clear, upfront requirements and verifiable outcomes that would take a junior engineer four to eight hours, and that because it can run in parallel without limit it suits work such as resolving vulnerabilities flagged by static analysis tools, language and framework migrations, writing unit tests and completing small tickets. It separately describes brownfield feature work, where existing code provides clear patterns for Devin to replicate and modify. For migrations, the post says that once Devin has instructions on how to update each repository, a fleet of Devins can execute on every repository in parallel; for test generation, humans write a unit-testing playbook, a fleet of Devins writes the tests, and code owners then check that all logic has been tested. Cognition limits its pull-request review role to a first pass that catches obvious issues, stating that human review remains necessary because code quality is not straightforwardly verifiable.

On understanding, the same post describes Devin documenting large codebases through DeepWiki and helping engineers plan through a chat interface (AskDevin) that can explain a system with architecture diagrams, map dependencies, flag breaking changes and recommend what should be tackled by humans versus AI.

The post names three areas for improvement. Devin cannot independently carry an ambiguous project end-to-end on its own judgement, and needs specifics — in visual design, component structure, colour codes and spacing values. It handles clear upfront scoping well but usually performs worse when given more instructions after a task has started, so the post places more responsibility on engineers to scope work up front and to learn to "manage" Devin. And while it collaborates in Slack, Teams and Jira, it cannot manage reports or stakeholders. These are Cognition's characterizations of its own product.

## Enterprise Administration

The Mercari post is the fullest description this wiki holds of Devin's administrative surface, and it is written from the operator's side rather than the vendor's. Under the Enterprise plan, multiple Organizations are managed centrally through an Enterprise management layer, rather than sharing a single Organization as on the Core or Team plans — the features that led that team to choose it were SSO through Okta, audit logs, permission management, and environment isolation per team.

Management is exposed through two API versions. The post describes v3 as the latest Enterprise management API, allowing management of Members, Roles, Secrets and Knowledge at both Enterprise and Organization levels, and documented as REST APIs with detailed request and response specifications; it states that Devin released v3 in late 2025 and added Secret management to it in January 2026. That team built its automation on v3 and used the v2 API for API key management alone, v2 allowing creation, retrieval and deletion of API keys across multiple Organizations. It uses the v3 Enterprise Audit Logs endpoint, which it says differs from the v2 endpoint in having pagination.

The post names three things the product did not provide at the time of writing, each of which that team had to build around: there is no official Terraform provider, so it wrote its own using the Terraform Plugin Framework; Devin does not offer expiration management for API keys as a standard feature, so long-lived keys can otherwise remain in each Organization; and Devin has no OIDC token issuance feature that would let it work with Workload Identity Federation, so Google Cloud access requires service account keys. Usage is bounded by ACU (Agent Compute Unit) limits, which that team sets per Organization and per session to prevent unexpected cost overruns. Its overall assessment is that the v3 API already includes the endpoints required for Enterprise administration, while management requirements not covered by standard features had to be supplemented with custom tools.

## Adoption & Ecosystem

[[Organization/mercari]] rolled it out to multiple teams across the company on the Enterprise plan, assigning Organizations by team or purpose so that each team's information stays isolated, and was running more than ten Organizations with a large number of users at the time of that post. That is one company's deployment, reported by the team that administers it.

The Yayoi team's deployment is a different shape: Devin is wired into GitHub Actions as a reviewer, triggered when a pull request is opened, updated or reopened and gated to exclude drafts and forks, working from a review-perspective file committed to the repository. That account reports the limits as concretely as the benefits — insufficient grasp of project context producing off-target findings, and false positives on matters the project has deliberately accepted — and names the Knowledge feature as where it intends to record cases judged not to be problems, so the same finding is not raised repeatedly. That intention is stated as the team's direction rather than as an established practice.
