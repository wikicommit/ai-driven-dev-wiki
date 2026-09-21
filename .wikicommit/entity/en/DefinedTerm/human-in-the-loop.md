---
title: "Human-in-the-loop"
type: "schema:DefinedTerm"
lang: en
tags: []
sources:
  - type: url
    url: 'https://addyosmani.com/blog/coding-agents-manager/'
    hash: sha256:fc697c3fcc830075a1a6b6751a1f242d4b6ff4ea9a385c1ec60a0c6f8a6e50a1
  - type: url
    url: 'https://addyosmani.com/blog/long-running-agents/'
    hash: sha256:fa154fd01c14b8301d6ace42af061e437332617df2059253633747e4f7d39b17
  - type: url
    url: 'https://arxiv.org/pdf/2604.16520'
    hash: sha256:2601c1408563f747b2ac732af43342b6d4d14231aace9b4a2e0aa4d33ba3f674
  - type: url
    url: 'https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf'
    hash: sha256:9d619ed7dd7cb94569658ca3de72615ef792761e6e4147e36c45edf2f945bbf9
  - type: url
    url: 'https://hoop.dev/blog/human-in-the-loop-approval-in-ai-coding-agents-explained'
    hash: sha256:d47e37ed6d4309cb36f68927dfc4477de6d95bb29a757d4457974ee26a438f58
  - type: url
    url: 'https://www.port.io/blog/human-in-the-loop-for-ai-coding-agents'
    hash: sha256:766abcbeb6946c92580399d54cd8330c0edeb8fda6e8e61aefb36579d744524c
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/62639/'
    hash: sha256:8fe61a90b7d83235354ba7e66eb8068f7329ab03406aa10fc3725f34ee02cadc
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "A design in which a human is deliberately kept part of an otherwise-automated agent workflow, rather than letting the agent run unsupervised. This wiki's sources use the one term for seven distinct patterns: real-time pairing, an asynchronous approval gate inside a long run, a structured review surface for inspecting and editing proposals, an escalation path an agent takes when it cannot finish, a network gateway that holds the credential and forwards a request only on consent, a selection mechanism deciding which actions pull a human in at all, and a ratification step in which the AI proposes candidates and only a human decides which become team norms."
---

Human-in-the-loop describes a design in which a human is deliberately kept part of an otherwise-automated agent workflow, rather than letting the agent run entirely unsupervised. The term is used for seven distinct patterns across the sources: a developer pairing with an agent in real time, an asynchronous approval gate inside a longer autonomous run, a structured review surface through which a person inspects and edits what the agent proposes, an escalation path the agent takes when it cannot complete a task on its own, an enforcement point placed in the network path between the agent and the system it is acting on, a selection mechanism that decides which actions pull a human in at all, and a ratification step in which the AI proposes and the human alone decides what becomes a standing rule.

## Usage

In the real-time sense, Osmani places human-in-the-loop sessions on one side of a two-mode mental model for working with coding agents: local, high-touch sessions where a developer stays engaged, course-correcting as the agent works and making calls that require context the agent lacks — architecture decisions, tricky refactors, product nuance, ambiguous requirements — as opposed to cloud or background sessions that run asynchronously on bounded, well-specified tasks such as straightforward features, migrations with clear patterns, test generation, documentation updates, dependency bumps, and targeted refactors.

A later post on long-running agents uses the same term for a different pattern: delegated approval inside an agent that otherwise runs unsupervised for hours or days. It contrasts this with what it calls the common but weak implementation of "human-in-the-loop" — serialize state to JSON, fire a webhook, and hope someone responds, after which the state goes stale, the notification gets buried, and the agent re-deserializes into a slightly different world. Long-running runtimes are described as instead letting the agent pause in place with its full execution state intact (reasoning chain, working memory, tool history, pending action), consuming zero compute while hours of human time pass, and resuming with sub-second latency once a decision is made. Google's Mission Control is named as one vendor's implementation of this pattern, with the post stating the underlying pattern works regardless of vendor.

[[ScholarlyArticle/agentclick]] adds a third emphasis: that whether a human is nominally in the loop matters less than what the interface lets them actually do. Its authors argue that terminal output interleaves reasoning traces, tool logs and proposed actions in a single stream, so it is hard to identify what requires review; that feedback is cumbersome because users must type free-form corrections even for small local edits; and that consequential actions are presented as opaque events or binary prompts, leaving little room for targeted inspection or modification. Their response, [[SoftwareApplication/agentclick]], is a review layer whose stated aim is to improve collaboration rather than merely gate execution: the user can approve, edit directly, delete content, adjust constraints or request a targeted rewrite at the level of the artifact under review, which those authors argue matters most when an agent's output is largely correct but needs a localized change. They also describe review as a channel for preference capture, with reason-tagged edits written to a memory file the agent reads in later runs, so a correction shapes future behaviour rather than serving as a one-off override.

[[TechArticle/a-practical-guide-to-building-agents]] arrives at the term from a fourth direction, as
the last item in its treatment of [[DefinedTerm/guardrails]]. There, human intervention is a
mechanism that lets an agent gracefully transfer control when it cannot complete a task — escalating
to a human agent in customer service, or handing control back to the user in the case of a coding
agent. OpenAI presents it as especially important early in deployment, where it helps identify
failures, uncover edge cases and establish an evaluation cycle, and frames it as a way to improve an
agent's real-world performance without compromising the user experience.

A fifth position is that the gate belongs neither in the agent nor in the review tooling but in the
data path between them. The vendor hoop.dev argues that an agent authenticating directly against a
Git server, container registry or CI/CD orchestrator gives identity verification but no point at
which a policy can pause, inspect or require a human decision, and that the operation is then
recorded only in the target's logs, if at all — and that a post-hoc pull-request review arrives too late, because the
artifact already exists in version control and may have exposed a secret or triggered downstream
jobs before anyone looks. Its answer is a Layer 7 gateway that receives the request, inspects the
payload at the protocol level, routes it to an authorized reviewer where policy demands, and
forwards it only on consent — recording the session and the decision as it goes. That argument
appears in a post promoting the vendor's own [[SoftwareApplication/hoop-dev]] gateway, so the
framing and the product are not separable here.

A sixth position keeps the definition and changes the question. Port's
[[BlogPosting/do-you-really-need-a-human-in-every-loop]] gives the term a narrow working
definition — an oversight model in which agents do the work but cannot make irreversible
changes without a human's approval — and then argues that the phrase gets treated as a single
setting to turn on when it is really a pattern that has been shifting underfoot. Reviewing every
output was enough while agents only proposed changes; once they deploy services, restart workloads
and resolve incidents, reviewing every action does not scale, so what matters is no longer whether
a human is in the loop but what pulls the human in. Its answer is two kinds of guardrail that
decide in opposite ways: a [[DefinedTerm/rule-based-gate]], a deterministic condition written in
advance that fires the same way every time, and a [[DefinedTerm/risk-based-gate]], in which an
agent scores the specific action against live context and a human is pulled in only above a set
threshold. The test for choosing between them is whether the decision is a lookup or a judgment.
That argument appears in a post recommending the vendor's own [[SoftwareApplication/port]]
platform, so as with the fifth position the framing and the product are not separable here.

A seventh position moves the gate off the agent's actions entirely and onto the rules the agent
will later be judged by. In [[BlogPosting/automating-coding-guidelines-with-ai]], a CyberAgent
team has an AI harvest pull-request review comments into coding-guideline candidates and present
them as a pull request, where a person decides which are adopted. Its author's stated reason for
inserting the human is that a coding guideline is not a summary but a team norm, so "something
plausible-looking is written here" is not good enough. The specific hazard named is that review
comments can depend heavily on the context of the moment — circumstances particular to that
repository, the release priorities at the time, an implementation allowed as an exception, a
trade-off taken deliberately — and that an AI finalizing candidates without that context risks
leaving wrong guidelines standing. The division the post draws is therefore by role rather than
by risk: the AI is assigned the job of producing candidates, the human the job of deciding
whether one stands as a norm, which the author argues keeps speed while holding the validity of
the judgment.

## When It Applies

The real-time sense applies to work where taste and judgment dominate and the agent lacks context a person must supply as it goes — architecture decisions, tricky refactors, ambiguous requirements, nuanced product calls — and assumes a developer is available to actively pair with the agent rather than fire off a task and return to it later.

The delegated-approval sense applies to a long-running, otherwise-autonomous agent that reaches a decision point requiring a human sign-off, and assumes a runtime that can hold the agent paused in place with its full execution state intact — reasoning chain, working memory, tool history, pending action — rather than one that serializes state out, fires a notification and hopes for a reply. Its failure mode without that runtime is state going stale or a webhook notification getting buried before a human ever acts on it.

The artifact-review sense assumes an agent that can be made to submit proposals and wait for an outcome before acting, and a surface other than the terminal on which to render them. The AgentClick authors argue the barriers they identify fall hardest on non-expert users, and become sharper when agents run on remote or headless infrastructure where the terminal is not merely a poor collaboration medium but often an inaccessible one. That work is a demo paper whose three walkthroughs its own authors present as capability illustrations rather than a controlled user study, so the claimed benefits are demonstrated rather than measured.

The escalation sense is defined by its triggers rather than by a phase of work. OpenAI names two:
exceeding failure thresholds — limits set on agent retries or actions, such as failing to understand
a customer's intent after multiple attempts — and high-risk actions that are sensitive, irreversible
or high-stakes, its examples being cancelling user orders, authorizing large refunds and making
payments. It presents the second trigger as a standing requirement until confidence in the agent's
reliability grows, rather than as a permanent property of those actions.

The enforcement-point sense assumes the agent's traffic can be routed through a proxy that reads the
protocol it speaks — the vendor names Git, HTTP and "the relevant API" — and that the gateway,
rather than the agent, can hold the credential for the target service, which the vendor presents as
reducing the risk of credential leakage. What it relocates is not when the human is asked but where
the asking is enforced: the vendor's argument is that direct agent-to-target access offers no point
in the data path at which policy can pause, inspect or require a decision. It is also the sense
whose payoff is stated in audit terms — session logs, a record of who approved each change, and the
stored masked diff, exportable for compliance reporting — rather than in development terms.

The selection sense assumes that agents are already taking real, state-changing actions rather than
only proposing them — its stated failure case is a team that keeps gating only code merges and pull
requests, which Port reports half the room still doing when it surveyed engineering leaders at one
of its meetups. Both of its gates assume a live, connected view of the organisation's systems to
read from: the post's own summary is that a rule with no real data to check is a guess and a risk
score over thin context hides a bad guess behind a number, so a gate reading stale or partial
context makes confident, wrong calls. The risk-based half additionally assumes a threshold that
will be tuned over time, tracing of every decision including what the model scored and on what
context, and a fallback to blocking human review when the model is unsure. Its claims are the
vendor's own and are not accompanied by measurements.

The ratification sense is the one whose output is a rule rather than an action, so what it gates
differs from the rest: the decision is taken in batches, over a window of past review comments —
seven days by default in the CyberAgent workflow, on whatever schedule the calling repository
sets — rather than at the moment an agent wants to act. What it assumes is that the candidates
arrive in a form a person can rule on cheaply, which that implementation supplies as a pull
request listing each candidate with a priority, background and citation alongside an exclude
checkbox. Its stated failure mode is the one it was built to avoid rather than one
observed: a wrong guideline, adopted because the context that made a comment situational was not
visible at the point of decision. The reported effects — team perspectives beginning to show up
in AI review findings, human review shifting toward specification validity and business logic —
are the author's early observations of a recently introduced mechanism, with no measurement given.

## Related Terms

[[DefinedTerm/sandboxing]], [[DefinedTerm/checkpoint-and-resume]], [[DefinedTerm/long-running-agent]], [[DefinedTerm/approval-fatigue]], [[DefinedTerm/guardrails]], [[TechArticle/a-practical-guide-to-building-agents]], [[DefinedTerm/rule-based-gate]], [[DefinedTerm/risk-based-gate]], [[DefinedTerm/agentic-code-review]]
