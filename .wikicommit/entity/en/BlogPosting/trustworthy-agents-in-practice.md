---
title: "Trustworthy agents in practice"
type: "schema:BlogPosting"
lang: en
tags: [agent-safety, agent-architecture, human-in-the-loop, security]
sources:
  - type: url
    url: 'https://www.anthropic.com/research/trustworthy-agents'
    hash: sha256:7b2800e6840e79dc817c3f2b89dba0aad5a79482b920ffc7c6ff72b1b9f967c9
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "Anthropic's account of how its agent-trust principles turn into product decisions, built on a decomposition of an agent into four components — model, harness, tools and environment — each a source of capability and a point of oversight. It works through human control, goal understanding and attack defence, then names what it thinks only the wider ecosystem can supply."
  datePublished: "2026-04-09"
  publisher: "[[Organization/anthropic]]"
---

This post is about governance expressed as product decisions rather than as policy. It takes the five
principles from Anthropic's earlier trustworthy-agents framework — human control, alignment with human
values, securing interactions, transparency and privacy — and works through how three of them show up in
shipped features, with the other two described as running through each.

Its most transferable contribution is structural. An agent is decomposed into four components — the
**model**, a **harness** of instructions and guardrails, the **tools** it can call, and the
**environment** it runs in — and each is presented as both a source of capability and a potential point
of oversight. The argument attached to that decomposition is a corrective: most AI policy conversation
centres on the model, understandably, but a well-trained model can still be exploited through a poorly
configured harness, an overly permissive tool, or an exposed environment.

The post closes by naming three things it believes no single company can supply — shared benchmarks,
shared evidence about how agents are actually used, and open protocols — and arguing that these are
infrastructure rather than goodwill.

## Key Points

- The working definition of an agent is a model that directs its own processes and tool use rather than
  following a fixed script, operating in a self-directed loop: plan, act, observe the result, adjust,
  and repeat until the task is done or human input is needed.
- The four components are given concrete content: the harness might instruct the agent to flag anything
  over a set amount or never to submit expenses without user confirmation; tools are the services the agent can use;
  and the environment determines what files, websites and systems are reachable — the same agent on a
  corporate laptop inside a company network having different data access and different stakes than on a
  personal phone.
- The most direct form of human control described is per-action permissions: in Claude.ai and Claude
  Desktop users choose which tools to enable and configure each action as always allowed, needing
  approval, or blocked — so reading a calendar can be always-safe while sending an invitation still
  requires approval.
- The post names the failure mode of that approach directly: when a task requires dozens of actions,
  repeated prompts become friction and users sometimes tune them out.
- Plan Mode in [[SoftwareApplication/claude-code]] is presented as the response — the agent shows its
  intended plan up front, the user reviews, edits and approves the whole thing before anything happens,
  and can still intervene during execution. The stated effect is to shift oversight from the individual
  step to the overall strategy, which the post says is where users most want to exercise judgement.
- Subagents are named as an open problem for oversight rather than a solved one: work handed off to
  other agents running in parallel is no longer visible as a single thread of actions, and the post says
  Anthropic is exploring coordination patterns and will feed what it learns into how oversight is
  designed.
- On goal understanding, the post frames the difficulty as a calibration problem: an agent that stops at
  every possible question gives up the autonomy that makes it useful, while one that always pushes
  through risks misreading intent. The hard part is recognising which gaps it can resolve itself and
  which are questions of preference only the user can settle.
- Two training levers are named for this: constructing scenarios that place the model in ambiguous
  situations and reinforcing its choice to pause rather than assume, and Claude's Constitution, which
  the post says favours "raising concerns, seeking clarification, or declining to proceed" over acting
  on assumptions.
- Evidence offered for the effect: on complex tasks users interrupt the agent only slightly more often
  than on simple ones, but the agent's own rate of checking in roughly doubles.
- On [[DefinedTerm/prompt-injection]], the post states two scaling properties of the risk — the more open
  the environment, the more entry points exist; the more tools available, the more an attacker can do
  once inside — and gives this as the reason defences are built at several layers rather than one:
  training the model to recognise injection patterns, monitoring production traffic to block real-world
  attacks, and external red-teaming.
- Those safeguards are explicitly described as not a guarantee, which the post gives as the reason
  customers should think carefully about which tools and data they give an agent, which permissions they
  grant, and which environments they let it operate in — its stated general truth being that agentic
  security requires defences at every level and on choices made by every party involved.
- For the ecosystem it names three gaps. There is no rigorous standardized way to compare agent systems
  on prompt injection resistance or on how reliably they surface uncertainty — companies test their own
  systems with their own methods and none are independently verified — and the post suggests standards
  bodies such as NIST are well placed to maintain shared benchmarks and encourage third-party evaluation.
- The second gap is evidence sharing: Anthropic says it has published extensively on how Claude is used
  as an agent and where it struggles, and hopes this becomes common practice so policymakers have a
  fuller picture.
- The third is open standards. The post states Anthropic created
  [[DefinedTerm/model-context-protocol]] as an open standard for how models communicate with external
  data and tools, and has since donated it to the Linux Foundation's Agentic AI Foundation, on the
  reasoning that open protocols let security properties be designed into the infrastructure once rather
  than patched together per deployment, and keep competition focused on the quality and safety of the
  agent rather than on who controls the integrations.

## Context

This is a vendor describing its own product decisions and advocating for infrastructure it has a stake
in, and it should be read that way: the features are presented as illustrations of principles rather
than as evaluated interventions, and no effectiveness figures accompany the permission model, Plan Mode
or the layered injection defences. The one quantitative claim — that the agent's check-in rate roughly
doubles on complex tasks while user interruptions rise only slightly — is cited to Anthropic's own
earlier research on agent autonomy.

The post is unusually direct about unresolved problems for a piece of product communication. It calls
goal understanding one of the harder unsolved problems in agent development, states that subagent
workflows raise oversight questions it has not answered, and says plainly that its own safeguards are
not a guarantee. The recurring move is to push part of the responsibility outward — to the customer
choosing tools, permissions and environments, and to standards bodies supplying benchmarks nobody
currently has.
