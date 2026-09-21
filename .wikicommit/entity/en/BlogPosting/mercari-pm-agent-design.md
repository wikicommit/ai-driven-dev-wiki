---
title: "mercari-pm-agent Design — Automating the PM Workflow with Claude Code Skills and MCP"
type: "schema:BlogPosting"
lang: en
tags: [agent-skills, mcp, prompt-engineering, agent-evaluation]
sources:
  - type: url
    url: 'https://engineering.mercari.com/en/blog/entry/20260427-mercari-pm-agent-design-automating-the-pm-workflow-with-claude-code-skills-and-mcp/'
    hash: sha256:f446b9545db9ce2a51b98a91bfe525a706f8f22bd2381f38543f927626b9b58a
review_status: pending
generated_at: "2026-09-21"
generated_by: "claude-opus-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An internship account of building a product manager's end-to-end workflow as a Claude Code Skill, connecting Notion, Slack, an in-house data platform and Figma over MCP, and using a second skill to score the first one's output."
  author: ["Shogo Kikuchi"]
  datePublished: "2026-04-28"
  publisher: "[[Organization/mercari]]"
---

This post describes `mercari-pm-agent`, a [[DefinedTerm/agent-skills]] package the author built as a PM intern at Mercari, which handles within a single session the workflow a product manager goes through: problem discovery, data gathering, PRD creation and UI mockups. The post's focus is the design of that skill and the [[DefinedTerm/model-context-protocol]] connections behind it rather than the product outcome.

The problem it starts from is not access but assembly. Mercari PMs check mid-term strategy and KPI goals in Notion, search internal requests and feedback in Slack, review quantitative user metrics in Looker, look at current designs in Figma, and integrate all of it into a PRD. The post's point is that reaching each tool is not difficult in itself — what takes non-trivial time is organizing which data matters for the decision at hand while moving across them. Its view of where a PM's time should go instead is thinking deeply on the information gathered, making decisions, and having conversations with stakeholders; the author's stated motivation for building the tool is to shift time away from information gathering and toward thinking and decision-making.

Its most transferable claim is about prompt structure rather than about PM work. Having first consolidated everything into one `SKILL.md`, the author found through scoring that the longer the file, the worse the output accuracy became, and split behaviour definition from reference data accordingly. The post presents this as applying separation of concerns from software engineering to prompt design, and reports that the structural change alone produced a clear improvement in score.

## Key Points

- The skill is organized as a thin `SKILL.md` holding the agent's behaviour definition, plus a `references/` directory holding a PRD template, a nine-item PRD quality checklist, a UI-spec and Figma prompt template, a data interpretation guide, a data-source list and an output checklist. The stated division is that `SKILL.md` keeps only what to do and in what order, while concrete data and templates are referenced when needed.
- The author relates the long-file accuracy problem to the known phenomenon, often called "Lost in the Middle", where models fail to properly attend to relevant information in the middle of a long context, and notes that Anthropic's prompt engineering guidance also recommends keeping prompts concise.
- `SKILL.md` is written in English, the author's stated reason being that instructions in English tend to produce higher accuracy with Claude.
- Four MCP servers are connected, of which one is official and three were built in-house: Notion MCP, provided by Notion, for strategy documents and the KPI dashboard; a custom Slack MCP for posts from an internal feedback channel; Socrates, an in-house BigQuery and Looker platform, for metrics such as CVR; and a custom Figma MCP for component information from design files.
- Those MCP sources are queried in parallel during data collection, with a rule written into the data-source reference file instructing the agent not to wait for one source before querying another, and to skip a source silently and mark it in the output if it is unavailable. The stated effect is reduced waiting time compared to sequential access, plus fallback behaviour so the process does not stop when some MCPs are down.
- The Slack MCP setup requires internal VPN connectivity and a user token, which the author passes into Claude Code's configuration as an environment variable so the token string is not exposed in chat; because Slack user tokens expire in seven days, a separate refresh script was prepared.
- Evaluation criteria were defined before implementation — understanding accuracy, spec specificity, feasibility and UX validity — an approach the author compares to test-driven development and calls Prompt TDD. The stated reason is that with LLM-based agents it is harder to judge whether output is correct than whether it runs, so defining axes first allows improvement cycles based on criteria rather than intuition. Real web improvement topics were collected into an evaluation dataset.
- The post names plausible hallucination as the most dangerous risk of embedding an LLM in a business workflow: models can output reasonable-looking numbers where no data exists, and a PM who trusts them puts fiction into a PRD. Its stated position is that this cannot be solved by telling the model not to lie — constraints must specify how the model should behave when it recognizes missing data. The rules used are that unconfirmed data must be labelled "Not provided" or "To be validated", and that numbers and sources must never be fabricated.
- The agent is also prohibited from advancing to the next step without the PM's confirmation, by an instruction stating that it is not allowed to infer completeness and that only explicit confirmation from the PM allows progression. The author's stated purpose is to keep the PM as the decision-making driver rather than letting the agent auto-advance through a plausible flow.
- A separate evaluation skill sends test cases to the agent and returns scores for output quality. Iterating on those scores is what produced the shorter-file insight that drove the file-splitting change — the post's own description of this is using a skill to evaluate a skill.
- The author's closing learnings are that designing a skill is close to writing a behaviour specification, with constraints mattering more than commands; that MCP connections should be designed for parallelism with fallback and robustness considered together; that separation of concerns applies to prompt design because longer context lowers accuracy; and that evaluation criteria should be defined before implementation.

## Context

The post is written from an internship rather than from a team's production practice, and the tool it describes is internal. Its evidence is the author's own evaluation harness: scoring was done by a skill the same author wrote, run against a dataset the same author assembled. The post reports no numbers for the evaluation itself — the gain from splitting the file is described as a clear improvement in score rather than quantified.

Its claims divide into two kinds worth keeping apart. The observations about PM tooling at Mercari are particular to that company's stack. The design claims — that a shorter behaviour definition scores better than one long file, that constraints on how to behave when data is missing work where instructions not to fabricate do not, and that an agent should be barred from inferring its own completeness — are stated as general lessons about building agents on Claude Code Skills, and the author offers them as such.
