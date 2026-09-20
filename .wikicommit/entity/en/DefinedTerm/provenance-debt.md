---
title: "Provenance Debt"
type: "schema:DefinedTerm"
lang: en
tags: [technical-debt, licensing, attribution, accountability]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2606.14796'
    hash: sha256:326808613b90c63916547135da3cc5027f45d992bef8b64cc8f926069d4d622c
review_status: pending
generated_at: "2026-09-20"
generated_by: "claude-opus-5"
generated_with: "0.7.0"

properties:
  description: "Technical debt arising from unclear ownership or missing attribution in AI-generated code, creating legal and accountability challenges once that code becomes part of a larger software system."
---

Provenance debt — also called ownership debt — is the accumulation of unclear ownership or missing attribution in AI-generated code, creating legal and accountability challenges. [[ScholarlyArticle/faster-code-deeper-debt]] identifies it as one of six LLM-specific debt categories outside the established technical debt taxonomy it works from, and the least discussed of them: one formal source and one grey source in a review of 104.

The review is precise about what the category covers. The concern is not ownership of models or governance of datasets, but the traceability, attribution and licensing of the generated software artefacts themselves once they become part of a larger system.

## Usage

The grey literature source the review draws on frames the problem as responsibility and ownership for LLM-generated logic becoming unclear as code cloning becomes more common with the use of AI tools. The formal source examines whether LLM-generated code includes links or citations to its sources and concludes that such tools often lack clear attribution — which is where the term comes from in that study, and which raises questions about code ownership and licensing.

The review notes that this topic remains underexplored compared with more traditional forms of debt, and its own source counts bear that out.

Tooling relevant to it is beginning to appear at the edges of the review's evidence. GitHub Copilot is described as gradually introducing responsible AI features including reference citations alongside flagging of insecure or biased outputs, and the review lists it among AI coding assistants that provide additional features beyond generation.

## When It Applies

Provenance debt accrues wherever generated code enters a codebase without a record of where it came from, and its cost is deferred in a particular way: unlike code debt, which surfaces as maintenance friction, it surfaces as a legal or accountability question at the point where someone needs to establish who is answerable for a piece of logic or under what terms it may be distributed.

The practitioner-facing mitigation the review names is provenance review as a safeguard — asking where the code came from — alongside governance checks and systematic prompt documentation, offered as ways to reduce long-term risks rather than as a solution to the attribution problem itself.

The category rests on very thin evidence within this review, and the authors present it as an area needing attention rather than as a settled finding. A related formal source the review cites treats accountability more broadly, describing ethical debt as the accumulation of unresolved ethical risks in AI-assisted development and highlighting the mapping of accountability across developers, AI systems and organisations as needing more attention in future research.

## Related Terms

- [[DefinedTerm/governance-debt]]
- [[DefinedTerm/prompt-debt]]
- [[DefinedTerm/fast-integration-debt]]
