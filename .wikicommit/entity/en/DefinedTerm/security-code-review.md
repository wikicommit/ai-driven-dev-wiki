---
title: "Security Code Review"
type: "schema:DefinedTerm"
lang: en
tags: [code-review, security]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2401.16310'
    hash: sha256:68d2fba8f757c9789995cbb7728c6a9074f36cf7747bdaba59f8d6721cbfc647
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Security analysis carried out in the context of code review: reviewers examine code submitted by a developer for security defects before it is merged into the repository, raising issues, discussing them with the developer and recommending fixes."
---

Security code review is security analysis performed in the context of code review, the human-intensive process in which a reviewer examines code submitted by a developer to detect bugs, verify the implementation against its specification, ensure compliance with guidelines and ensure quality, raising issues, discussing them with the developer and providing recommendations. Applied to security, it aims to catch security defects — potential risks or weaknesses introduced during implementation — before they are merged into the source code repository. The term and this framing are taken from [[ScholarlyArticle/an-insight-into-security-code-review-with-llms]], which in turn attributes the name to earlier work.

## Usage

According to that study, many organizations are shifting security analysis to earlier stages of software development, typically to code review time, and security code review is increasingly integrated into project teams' development pipelines; it argues that bringing security analysis into code review combines the viewpoints of reviewers and developers and helps prevent defects that programmers working alone introduce. It is resource-intensive, needing significant human effort and time to review and revise code, which the authors describe as a notable challenge in large open-source projects with many contributions and as the motivation for automated tools to assist reviewers. The study notes that static, dynamic and hybrid program analysis tools and machine-learning approaches each face practical problems such as imprecision, high false positive rates and poor generalization, and it evaluates large language models as assistants that can locate, describe and suggest fixes for defects.

## When It Applies

Security code review assumes a code review process in which changes are examined before merging, and reviewers with enough security knowledge to recognise defects. The study found that the LLMs it tested significantly outperformed static analysis tools on real reviewer-identified defects but still fell significantly short of manual security code review, so it recommends using them as auxiliary tools in a multi-layered strategy in which reviewers confirm LLM findings on easier code and use them as a reference for deeper analysis of harder code. That recommendation is the authors' proposal based on one study of four open-source projects, not an established practice.

## Related Terms

- [[DefinedTerm/agentic-code-review]]
