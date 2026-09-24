---
title: "Human–Agent Cell"
type: "schema:DefinedTerm"
lang: en
aliases: ["HAC", "Human-Agent Cell"]
tags: [agentic-software-engineering, human-agent-collaboration]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2609.04630'
    hash: sha256:b89995b073da21f1e6d786f61dc056209cbca90ea6c15505e774483a51c9963e
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An execution abstraction proposed by Wang and Liu: one human execution subject together with their personal agents, local context, tools, delegated permissions and resource budget, treated as the practical unit that performs software work in an agentic setting — producing candidate changes, proposals and evidence without thereby gaining authority to accept them."
---

The Human–Agent Cell (HAC) is the execution unit proposed in
[[ScholarlyArticle/software-engineering-in-the-agent-era]] because, in that paper's words, the word
"developer" no longer fully describes the execution unit that actually performs software work once agents
are involved. A HAC centres on one human execution
subject and combines that person's set of personal agents, their local working memory or context, the
available toolset, delegated permissions and a resource budget. It may use one agent or run several
specialized agents concurrently; changing a model version, adding agents or changing a token budget does
not usually create a new HAC, whereas a material change in the human subject or the formal engineering
boundary is treated as a handoff, termination or redefinition of the cell.

## Usage

The paper gives the HAC a minimal formal interface. Its inputs are a snapshot of the authoritative
engineering state, a task-and-resource contract and signals that the authoritative state has changed; its
outputs are a candidate change, proposals to change the authoritative state, and local evidence. Inside
that boundary the cell may hold substantial local information — scratch memory, provisional analyses,
debugging hypotheses, unaccepted designs — but this is execution state, not organizational truth: a
proposal becomes an organizational fact only through authorized acceptance followed by a versioned
commit.

The central point of the abstraction is the separation between execution and acceptance. A HAC produces
work, but execution alone does not confer authority to accept it. That authority belongs to
responsibility anchors under the organization's [[DefinedTerm/responsibility-topology]]; a HAC holds final
acceptance authority only if its human subject also holds the required formal authority. The same person
can be both a HAC's execution subject and an anchor for some domain, or can execute under another
anchor's authority, and the paper keeps the two counts distinct. Several HACs working in parallel will
naturally hold different contexts, so their candidates can each be locally coherent yet mutually
incompatible — the pressure the paper answers with shared authoritative state and context invalidation.

## When It Applies

The paper studies the HAC as the human-centred execution boundary in agentic software work, in which one
human execution subject works with one or more agents. It does not claim it is the only possible execution unit: team-level, organization-level or fully
autonomous agents may exist outside any HAC while remaining subject to the same distinction between
execution authority and acceptance authority. It also cautions that separate HACs are an execution
boundary, not a guarantee of independent judgment, since different cells may share models, tools and
retrieval sources and so fail in the same way. Like the paper's other constructs, it is proposed as part
of a theory awaiting empirical testing.

## Related Terms

[[DefinedTerm/trustworthy-change]], [[DefinedTerm/responsibility-topology]]
