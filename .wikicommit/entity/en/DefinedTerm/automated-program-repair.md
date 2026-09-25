---
title: "Automated Program Repair"
type: "schema:DefinedTerm"
lang: en
tags: [program-repair, debugging]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2403.17134'
    hash: sha256:aafce2ddc1642de21ae7f1c9a81dae3d270cea048a82a78f1d2819b04e881cc1
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "Automated program repair (APR) is the automatic fixing of software bugs, which promises to greatly reduce the time and effort that fixing bugs manually demands. Approaches range from fix patterns and symbolic constraints to machine-learning models and, most recently, large language models."
---

Automated program repair (APR) is the automatic generation of fixes for software bugs, addressing the need for effective and efficient bug resolution without the considerable time and effort that manual fixing demands. As described in [[ScholarlyArticle/repairagent-an-autonomous-llm-based-agent-for-program-repair]], researchers and practitioners have approached it with techniques based on manually designed and (semi-)automatically extracted fix patterns, symbolic constraints, and various machine-learning approaches, and APR has been deployed in industrial contexts.

## Usage

The RepairAgent paper describes the current state of the art as revolving around LLMs, in two generations: a first that interacts with the model once, giving it a prompt containing the buggy code and receiving a fixed version, and a second, iterative generation that queries the model repeatedly and adds compilation errors, test failures or other output from previous fix attempts to the next prompt. It argues that such hard-coded feedback loops do not let the model gather information about the bug or search the code base for repair ingredients — code fragments that could become part of a fix — and proposes treating the LLM as an autonomous agent that decides which tools to invoke instead. Beyond functional bugs, the same paper notes techniques targeting syntax errors, performance bugs, security vulnerabilities, type errors, common issues in deep-learning code and build errors.

Evaluations in the field commonly report two counts: plausible patches, which pass all test cases but are not necessarily correct, and correct patches, judged by matching or being semantically equivalent to the developer's fix. The RepairAgent paper notes that, as common in the field, it assumes perfect fault localization by default — that the lines to be edited are known — and that different approaches tend to complement each other, each fixing some bugs the others miss.

## Related Terms

- [[DefinedTerm/self-repair]]
- [[DefinedTerm/ai-coding-agent]]
