---
title: "Does every agent action need a human?"
lang: en
kind: debate
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"
derived_from:
  - path: .wikicommit/entity/en/DefinedTerm/human-in-the-loop.md
    source_commit: dd9449729978a2bb341016b5d35f2f19ff11a7a4
  - path: .wikicommit/entity/en/BlogPosting/do-you-really-need-a-human-in-every-loop.md
    source_commit: 6b5a8ac7a493c71300dccb7564cd1bdadb65f53c
  - path: .wikicommit/entity/en/DefinedTerm/rule-based-gate.md
    source_commit: 6b5a8ac7a493c71300dccb7564cd1bdadb65f53c
  - path: .wikicommit/entity/en/DefinedTerm/risk-based-gate.md
    source_commit: 6b5a8ac7a493c71300dccb7564cd1bdadb65f53c
  - path: .wikicommit/entity/en/DefinedTerm/approval-fatigue.md
    source_commit: 07f44d78c36c0f3ef8211927eac4fa818f178ac1
  - path: .wikicommit/entity/en/DefinedTerm/automation-bias.md
    source_commit: 6b5a8ac7a493c71300dccb7564cd1bdadb65f53c
  - path: .wikicommit/entity/en/DefinedTerm/sandboxing.md
    source_commit: 07f44d78c36c0f3ef8211927eac4fa818f178ac1
  - path: .wikicommit/entity/en/TechArticle/model-ai-governance-framework-for-agentic-ai.md
    source_commit: 6b5a8ac7a493c71300dccb7564cd1bdadb65f53c
  - path: .wikicommit/entity/en/ScholarlyArticle/magentic-ui.md
    source_commit: fed0100a95b9cbca3a6a11c43d68e28bc873bdea
  - path: .wikicommit/entity/en/BlogPosting/claude-code-for-web-async-coding-agent.md
    source_commit: d3a6cc04042ea62012d6cdb8d9075c83b708d517
---

Whether a human has to approve what an AI agent does is answered differently across this wiki's pages. Some place a person at named checkpoints and treat that as a standing requirement for certain actions; some argue that reviewing every action stops scaling once agents act in production and that the real question is what pulls a human in; and some argue that per-action approval is itself unreliable, so safety has to come from somewhere other than the person clicking "approve". This page sets those answers side by side with what each rests on. It does not settle between them.

The term at the centre, [[DefinedTerm/human-in-the-loop]], is itself used for seven distinct patterns across the sources — real-time pairing, an asynchronous approval gate inside a long run, a structured review surface, an escalation path, a network gateway, a selection mechanism, and a ratification step — so part of the disagreement below is about which of these a source means.

## Answer one: a human at named checkpoints

The first answer keeps a human approval step and specifies where it goes.

[[TechArticle/a-practical-guide-to-building-agents]], as relayed on [[DefinedTerm/human-in-the-loop]], treats human intervention as an escalation mechanism with two triggers: exceeding failure thresholds, such as repeated failure to understand a customer's intent, and high-risk actions that are sensitive, irreversible or high-stakes — its examples being cancelling orders, authorising large refunds and making payments. It presents the second trigger as a requirement until confidence in the agent's reliability grows, not as a permanent property of those actions, and calls human intervention especially important early in deployment.

[[TechArticle/model-ai-governance-framework-for-agentic-ai]] likewise asks for significant checkpoints that require human approval — high-stakes actions, irreversible actions, outlier behaviour, and user-defined thresholds — and asks that approval requests be contextual and digestible rather than raw logs.

What backs this answer in the grounding pages is mostly the stated risk of the action itself. One piece of empirical support comes from [[ScholarlyArticle/magentic-ui]]: in 24 internal adversarial scenarios, none were effective against the default configuration, which the paper attributes to layered mitigations — action guards requiring user approval, sandboxed execution, and a separate browser. With those mitigations deliberately disabled, prompt injection proved a more reliable exploit, and the authors were able to get the system to log into its own web interface and approve actions autonomously. The approval guard there is one layer among three, so this result does not isolate the contribution of the human step alone.

A different version of the same answer places the human not on actions but on judgment the agent cannot supply. Osmani's real-time sense, on [[DefinedTerm/human-in-the-loop]], reserves high-touch sessions for architecture decisions, tricky refactors and ambiguous requirements. The CyberAgent ratification step described there gates rules rather than actions: an AI proposes coding-guideline candidates and only a human decides which become team norms, on the stated reasoning that a guideline is a team norm and review comments may depend on context the AI cannot see.

## Answer two: not every loop — decide what pulls the human in

[[BlogPosting/do-you-really-need-a-human-in-every-loop]] answers its own title with a no. Its account is that putting a person in front of everything an agent does worked while agents only suggested code, but holds teams back once agents deploy services, restart workloads and resolve incidents. It reports that half the room at a Port meetup of engineering leaders still gate only code merges and pull requests, which it describes as breaking the moment an agent does something a pull request never covered.

Its reframing is that the question is not whether a human is in the loop but what pulls the human in, and it offers two gates that decide in opposite ways:

- A [[DefinedTerm/rule-based-gate]] is a condition written in advance that fires the same way every time — service tier, a Friday release freeze, data classification. Its stated strengths are predictability and auditability; its stated limit is that a rule is only as smart as the conditions you thought to write.
- A [[DefinedTerm/risk-based-gate]] has an agent score the specific action against live context — blast radius across a dependency graph, incident severity, whether a deploy is anomalous for a given service — and pulls in a human only above a threshold. It is said to need a tuned threshold, tracing of every decision, and a fallback to blocking human review when the model is unsure.

The choosing test is lookup versus judgment, and the post expects most teams to run both. Its unifying claim is that both gates are only as trustworthy as the context underneath them. The rule-based and risk-based gate pages both note that this is one vendor's formulation, advanced in a post recommending that vendor's own [[SoftwareApplication/port]] platform, and the selection-sense account on [[DefinedTerm/human-in-the-loop]] states its claims are not accompanied by measurements.

This answer and the first are closer than the titles suggest: Port's own working definition of human-in-the-loop is an oversight model in which agents cannot make irreversible changes without a human's approval, which overlaps with the irreversible-action checkpoints in answer one. Where they part is on how the trigger is decided — named classes of action and behaviour set out in advance, or a mix of written rules and live risk scoring by an agent.

## Answer three: per-action approval is unreliable, so reduce it

The third answer questions whether a human approval step does what it is meant to do.

[[DefinedTerm/approval-fatigue]] relays, via [[ScholarlyArticle/dive-into-claude-code]], Anthropic's analysis that users approve approximately 93% of permission prompts in [[SoftwareApplication/claude-code]], and reads that as making interactive confirmation behaviourally unreliable as a sole safety mechanism. The same source relays longitudinal data in which auto-approve rates rise from roughly 20% at fewer than 50 sessions to over 40% by 750 sessions, and an estimated 84% reduction in permission prompts from sandboxing. Its architectural conclusion is that a system must stay safe independently of human vigilance, and that the response to unreliable approval is to reduce the number of decisions humans must make. [[BlogPosting/ai-coding-agent-speed-and-safety-2026]], also relayed there, states the same mechanism from practice: past a certain number of approvals, people approve without looking, so security falls rather than rises.

[[DefinedTerm/automation-bias]] reaches a parallel point from governance. The IMDA framework states that requiring human approvers to continuously oversee agents can itself produce automation bias and alert fatigue; the automation-bias page reads this as meaning that adding approval points can make the problem worse rather than better. Its response is to measure oversight rather than assume it — a low override rate may indicate rubber-stamping, short review times may indicate automation bias — and to complement approvals with automated monitoring and denial by default when approval infrastructure fails.

What this answer puts in place of per-action approval is [[DefinedTerm/sandboxing]]: defining a boundary within which the agent works freely, and reviewing the result rather than each step. [[BlogPosting/claude-code-for-web-async-coding-agent]] reads Anthropic's sandboxing work as an acknowledgement that agents run without step-by-step approval are far more productive than agents that require it, making convenient safe execution — not tighter approval — the problem to solve; its author calls this the only approach to agent safety that feels credible to him. Even here, a human confirmation remains at one point: the out-of-sandbox proxy handles user confirmation for newly requested network domains.

The empirical backing for this answer is the approval-rate figures, relayed second-hand through a paper; only the 93% figure is tied to Claude Code, and neither the 84% figure nor the longitudinal data is tied to a named product on that page. The sandboxing page also records scepticism about how reliably agents' own sandboxes are implemented, as an author's assessment rather than a tested finding.

## Where the answers split

Laid side by side, the three answers disagree on different points rather than on one:

| | Human approval is… | What decides when a human is asked | Main backing in the grounding pages |
|---|---|---|---|
| Named checkpoints | a required control for certain action classes | the class of the action (irreversible, high-stakes, outlier, user-defined threshold) or the kind of work (judgment, team norms) | the stated risk of the action; one adversarial test where approval was one of three layers |
| What pulls the human in | necessary for some actions, but not scalable for all | a written rule or a live risk score | a vendor argument without measurements |
| Reduce the decisions | behaviourally unreliable as a sole mechanism | a boundary set in advance (the sandbox), with the result reviewed afterwards | approval-rate figures relayed second-hand — one from Claude Code, the others from publications the paper cites |

Some points are shared across all three. None of the grounding pages argues for approving every action without qualification. The IMDA framework appears on both sides of the split: it asks for human approval checkpoints and, in the same document, warns that continuous approval produces automation bias. And the fatigue argument and the gate argument both treat the number of prompts as a design variable — one reduces it by containment, the other by selection.

Other positions on the [[DefinedTerm/human-in-the-loop]] page move the question elsewhere rather than answering it: [[ScholarlyArticle/agentclick]] argues that what the review interface lets a person do matters more than whether they are nominally in the loop, and the hoop.dev gateway argues that the gate belongs in the network path between agent and target. The long-running-agent account there adds that an approval gate is only as good as the runtime's ability to pause in place while a human decides.

## Related pages

[[DefinedTerm/guardrails]], [[DefinedTerm/permission-modes]], [[DefinedTerm/deny-first-permission-evaluation]], [[DefinedTerm/supervised-agency-spectrum]], [[DefinedTerm/lethal-trifecta]]
