---
title: "Agent autonomy level schemes compared"
lang: en
kind: comparison
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"
derived_from:
  - path: .wikicommit/entity/en/DefinedTerm/supervised-agency-spectrum.md
    source_commit: 0ea12caf5df433486d9ab0e30d7c6a7b7cf57315
  - path: .wikicommit/entity/en/DefinedTerm/ai-maturity-levels.md
    source_commit: 55ede569cda46919557ac84eb1e8680542150b12
  - path: .wikicommit/entity/en/DefinedTerm/action-space.md
    source_commit: 6b5a8ac7a493c71300dccb7564cd1bdadb65f53c
  - path: .wikicommit/entity/en/DefinedTerm/four-stage-evolution-of-agentic-engineering.md
    source_commit: 0ea12caf5df433486d9ab0e30d7c6a7b7cf57315
  - path: .wikicommit/entity/en/DefinedTerm/se-autonomy-levels.md
    source_commit: 1241f6026eea3b9fe7666601cd9fbf68d202989f
  - path: .wikicommit/entity/ja/DefinedTerm/agentic-autonomy-levels.md
    source_commit: e4af5e5774ea7fb994b68ed1a084413f742a287b
  - path: .wikicommit/entity/ja/BlogPosting/agentic-autonomy-levels.md
    source_commit: e4af5e5774ea7fb994b68ed1a084413f742a287b
---

This wiki records several schemes for saying how far AI is trusted to act on its own in software work. They come from different kinds of source — three papers (one of them a position paper), a governance framework, a blog post, and a company's internal model — and they share some vocabulary ("assist", "agency", "autonomy", "levels"). They do not agree on what is being graded, how many positions there are, or where today's tools sit. This page sets them side by side so those differences are visible. It does not rank the schemes or recommend one.

## The schemes

- [[DefinedTerm/se-autonomy-levels]] — a six-level hierarchy, Level 0 to Level 5 (SE1.0–SE5.0), proposed in [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] and explicitly paralleled with the SAE levels of self-driving automation.
- [[DefinedTerm/agentic-autonomy-levels]] — a six-level scale, Level 0 (Assist) to Level 5 (managed-by-exception orchestration), built from two axes and presented in [[BlogPosting/agentic-autonomy-levels]] as a revision of Steve Yegge's single-axis ladder.
- [[DefinedTerm/supervised-agency-spectrum]] — five positions on one axis (assist, shadow, human-in-the-loop gate, bounded, full), used by [[ScholarlyArticle/from-determinism-to-delegation]] to argue that autonomy is not binary.
- [[DefinedTerm/four-stage-evolution-of-agentic-engineering]] — a four-stage roadmap with date ranges, from tool-augmented assistance to self-evolving ecosystems, proposed in [[ScholarlyArticle/agentic-software-restructuring-paradigm]].
- [[DefinedTerm/ai-maturity-levels]] — [[Organization/cyberagent]]'s internal model for grading product-development teams, from code completion (L1) to automation of the whole development process (L4).
- [[DefinedTerm/action-space]] — not a ladder itself, but the governance framework it comes from, [[TechArticle/model-ai-governance-framework-for-agentic-ai]], places autonomy on a four-point spectrum of human involvement and holds it apart from a second quantity, action-space.

## At a glance

| Scheme | What is graded | Positions | Kind of scheme |
|---|---|---|---|
| SE Autonomy Levels | AI involvement in software engineering, by what the system maps from and to | 6 (Level 0–5) | Classification, anchored on the SAE levels |
| Agentic Autonomy Levels | An AI coding agent, or a group of them | 6 (Level 0–5), read as one climb over two axes | Classification |
| Supervised Agency Spectrum | A deployment's position between human and agent authority | 5 | Framing within a position paper |
| Four-Stage Evolution | Agentic engineering as a field, over time | 4 stages with date ranges | Forecast / roadmap |
| AI maturity levels | A product-development team | L1–L4 in one account, five levels in another | A company's internal adoption target |
| Autonomy vs action-space | An agent, on two independent axes | 4 points of human involvement | Risk-assessment framing |

## What counts as "autonomy"

The schemes use the same words for different things.

- **SE Autonomy Levels** separate *agency* — the capacity to act and execute plans toward a given goal — from *autonomy* — the capacity to self-govern and independently formulate those goals. Each level is defined by what it maps from and to: editing intent to predicted tokens (Level 1), a planned change to a generated block of code (Level 2), a technical goal to a multi-step plan (Level 3), a domain mandate to concrete goals (Level 4), a general mandate to domain-specific mandates (Level 5).
- **Agentic Autonomy Levels** also use the word *agency*, but for how far a single agent is allowed to go before human judgment is needed. The second axis is not goal-setting but *orchestration*: how many agents run and who coordinates them.
- **The governance framework behind action-space** defines autonomy as the degree to which an agent decides how to act toward a goal — for example by defining the steps — set by how prescriptive its instructions are and by the level of human involvement. Its second axis is *action-space*: which tools the agent may use and its permissions on them. The two are treated as independent, illustrated with an agent that has more autonomy but a smaller action-space set against one with less autonomy but a larger action-space.
- **The Supervised Agency Spectrum** uses a single axis along which three things move together: human authority falls, agent initiative rises, and the governance burden grows.
- **The Four-Stage Evolution** characterises each stage on four axes: what the agent can do, the enabling technologies, the human role, and representative systems.
- **AI maturity levels** grade how wide a scope of work AI agents take on and how the boundary of responsibility between humans and AI shifts — a property of a team's process rather than of one agent.

## Where more than one agent enters

Multiple agents appear as a distinct step in two of the schemes. In Agentic Autonomy Levels, orchestration becomes the distinguishing factor only near the top: Level 4 is parallel delegation of independent parts of a task, and Level 5 has a manager agent assign work to worker agents under a defined policy and escalate only exceptions to a human. In the Four-Stage Evolution, Stage III (Multi-Agent Teams, 2026–2029) has specialised agents coordinate as teams mirroring human engineering organisations, with shared memory and observability becoming critical infrastructure.

The pages recording the other schemes describe their levels without a separate multi-agent position. SE Autonomy Levels specialise upward along domain instead: Level 4 specialises along a technical-stack or quality-attribute axis, and Level 5 generalises to any unfamiliar domain.

## The lowest and highest rungs

At the bottom, several schemes place completion or suggestion. SE Level 1 (Token Assistance) is IDE autocomplete; CyberAgent's L1 is inline completion in the IDE, with the human writing all the code; the Four-Stage Evolution's Stage I covers code completion among other assistant tasks. Agentic Autonomy Levels and the Supervised Agency Spectrum both start from a position named "assist" — in the former, the agent proposes actions and the human judges every one. SE Autonomy Levels alone also includes a level with no AI at all (Level 0, Manual Coding).

At the top, the schemes differ in whether the highest position is described as existing:

- SE Level 5 is stated not to exist yet and to be at the conceptual or research stage.
- The Four-Stage Evolution's Stage IV (2028+) gives its representative systems as prospective, and has human involvement shift to meta-level governance.
- The Supervised Agency Spectrum's "full" position is paired with the observation that most enterprise deployments in regulated domains operate to the left of "bounded" — an observation the page notes is stated without a supporting measurement.
- Agentic Autonomy Levels' Level 5 is described as an operating-system-like layer, with OpenAI's proposed Symphony orchestration design referred to as one example.
- CyberAgent's L4 (PRD to Production) is a target: the company aims for its product-development teams to reach Level 4 by 2028.

## Where named tools are placed

Two schemes name the same products and put them in different places:

| Tool | SE Autonomy Levels | Four-Stage Evolution |
|---|---|---|
| [[SoftwareApplication/github-copilot]] | Level 2, Task-Agentic | Stage I, Tool-Augmented |
| [[SoftwareApplication/claude-code]] | Level 3, Goal-Agentic — among agents said to aim for this level | Stage I, Tool-Augmented — named as representative |
| [[SoftwareApplication/devin]] | Level 3, Goal-Agentic — among agents said to aim for this level | Stage II, Single-Task Autonomous — named as demonstrating autonomous feature work |

The two schemes define these positions differently — SE Level 3 by mapping a technical goal to a multi-step plan, Four-Stage Stage I by assistant work within human-led workflows — and the SE paper's wording is that these agents *aim for* Level 3. Neither grounding page comments on the other's placement. The Four-Stage page notes that nothing in its source reconciles its stages with other schemes, and advises treating its stage numbers as internal to that paper.

## What each scheme is used to argue

- **SE Autonomy Levels** — that the immediate challenge is mastering Level 3, because the move from Level 2 to Level 3 shifts the human–computer relationship through workflow orchestration, trust and verification, and that disciplined practice for goal-agentic systems has to come before Levels 4–5.
- **Agentic Autonomy Levels** — that a single number cannot express both an individual agent's trust level and the skill of coordinating many agents. The same post argues that the cap on autonomy for a task should be set by risk and reversibility rather than by task type, proposes a pre-run "contract" (goal, scope, non-goals, tools/permissions, stop conditions, evidence, escalation, budget), three diagnostic questions, and four autonomy anti-patterns.
- **Supervised Agency Spectrum** — that deployment should progress through graduated trust (shadow mode, human-in-the-loop checkpoints, bounded autonomy), and that because of [[DefinedTerm/compositional-reliability]], human checkpoints along a long task are what make autonomy usable at all.
- **Four-Stage Evolution** — a trajectory, read against the same paper's report that success rates on [[Dataset/evoclaw]] fall from above 80% on isolated tasks to at most 38% on continuous software evolution.
- **AI maturity levels** — that reaching L4 requires a shift to [[DefinedTerm/spec-driven-development]], because context design is the bottleneck L3 leaves and L4 removes.
- **Autonomy vs action-space** — that the two enter risk assessment on different sides: scope and reversibility of actions affect the *impact* of a failure, autonomy affects its *likelihood*.

The Agentic Autonomy Levels post and the governance framework both tie how much freedom an agent gets to reversibility, one as the cap on autonomy for a task and the other as a factor in a failure's impact.

## What stands behind each

- **SE Autonomy Levels** — proposed in a research paper, drawn by analogy with the SAE levels.
- **Agentic Autonomy Levels** — a blog post revising an earlier practitioner ladder; it cites two Anthropic research reports, including one on roughly 400,000 sessions finding that humans make about 70% of planning decisions while Claude carries out about 80% of actions.
- **Supervised Agency Spectrum** — one paper's figure and paragraph, not derived from a survey of deployments, with positions not defined by operational thresholds; the paper describes itself as a position paper.
- **Four-Stage Evolution** — a forecast whose stage boundaries are the paper's own reading of a trajectory, with overlapping date ranges that the paper does not comment on.
- **AI maturity levels** — a company's internal model, reported in two company blog posts that disagree on the scale's extent (four levels in one, five in the other).
- **Autonomy vs action-space** — a governance framework setting out concepts for risk management.

## Related

- [[DefinedTerm/human-in-the-loop]]
- [[View/does-every-agent-action-need-a-human]]
- [[View/multi-agent-orchestration-patterns-compared]]
