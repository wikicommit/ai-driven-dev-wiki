---
title: "RAGent"
type: "schema:SoftwareApplication"
lang: en
tags: [retrieval-augmented-generation, mcp]
sources:
  - type: url
    url: 'https://developers.cyberagent.co.jp/blog/archives/62048/'
    hash: sha256:b4ce4f9f18062c39d2f2b84a6b23e1c90c1bde712602bfa93006cf4549c21e28
review_status: pending
generated_at: "2026-10-04"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.8.0"

properties:
  description: "A retrieval-augmented generation (RAG) platform developed by SRG, CyberAgent's cross-organizational SRE group, that makes tools such as Kibela, Slack and spreadsheets searchable by vector search."
  applicationCategory: "RAG platform"
  author: "[[Organization/cyberagent]]"
---

RAGent is a retrieval-augmented generation (RAG) platform developed by SRG, the cross-organizational site
reliability engineering group at [[Organization/cyberagent]]. It turns a range of workplace tools — Kibela,
Slack and spreadsheets among them — into data sources that can be searched by vector search, so that past
documents and related knowledge can be looked up efficiently.

## Capabilities

RAGent indexes content from tools such as Kibela, Slack and spreadsheets for vector search and is reachable by
an AI agent through a [[DefinedTerm/model-context-protocol]] server (RAGent MCP).

## Adoption & Ecosystem

At WINTICKET it serves as the search layer for AI-assisted specification writing: [[SoftwareApplication/devin]]
queries it through RAGent MCP to find similar past specifications and to consult writing guidelines kept in
Kibela, alongside [[SoftwareApplication/deepwiki]] for reading code, as described in
[[BlogPosting/what-we-did-to-make-ai-stick-in-spec-writing-at-winticket]].
