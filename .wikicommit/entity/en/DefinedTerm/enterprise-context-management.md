---
title: "Enterprise Context Management"
type: "schema:DefinedTerm"
lang: en
aliases: ["ECM"]
tags: [ai-engineering, context, enterprise-data]
sources:
  - type: url
    url: 'https://www.codecentric.de/en/knowledge-hub/blog/ai-engineering-coding-loop-business-loop'
    hash: sha256:5e4a10e07a4ecd62092e6924b2fa7455a70c7bbb1e79bff049fdab61c177e240
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "Supplying AI agents' working loops with the right, current and permitted enterprise context — what business terms mean in a company, which data source is authoritative, which rules apply and which decisions were made — from a shared, governable source rather than from each agent's own version of the truth."
---

Enterprise Context Management is the practice of providing an AI-supported development loop with the right, current and permitted context from the surrounding enterprise, together with information on where that context comes from and how long it is valid: what terms such as customer, contract or revenue mean in a particular company, which data source is authoritative, which rules apply, and which decisions were made previously. In the account codecentric gives in its Loop Model of AI Engineering, it is the bridge that connects the Business Loop — what is built, why, and by what it is measured — to the technical Coding, Validation and Learning loops, so that domain knowledge, business needs and organisational constraints reach the coding loop and insights from development flow back into strategic decisions.

## Usage

The term is used this way in [[BlogPosting/from-coding-loop-to-business-loop-thinking-ai-engineering-holistically]], which notes that it is young and not standardised: some call the same thing [[DefinedTerm/context-engineering]] or a context layer. The post separates it from document search and classical retrieval-augmented generation, and states its architectural idea as not letting every agent build its own truth, but having all of them draw on a shared, governable context. Its FAQ goes further, claiming that without it the coding loop hallucinates even when the models are perfect.

## When It Applies

The post presents Enterprise Context Management as the answer to a failure it considers more common than technical failure: in codecentric's project experience, more AI initiatives fail at the connection to the business than at the technical loop, as when an insurer's AI-supported calculation logic turned out, three months before go-live, to rest on a business rule a regulatory change had already shifted. The post also names its limit: Enterprise Context Management makes bad enterprise data visible but does not correct it, so inconsistent master data, contradictory KPI definitions and unclear access rights become apparent only when an agent is supposed to use them. For that reason the post describes it as a maturity process rather than a product one installs. The framing is one consultancy's, drawn from its own project practice rather than from a measured study.

## Related Terms

- [[DefinedTerm/context-engineering]]
