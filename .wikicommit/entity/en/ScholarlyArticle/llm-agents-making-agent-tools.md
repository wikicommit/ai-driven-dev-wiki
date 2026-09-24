---
title: "LLM Agents Making Agent Tools"
type: "schema:ScholarlyArticle"
lang: en
tags: [agents, tool-use, benchmarks, evaluation]
sources:
  - type: url
    url: 'https://aclanthology.org/2025.acl-long.1266.pdf'
    hash: sha256:e540f7778ba7b71c57f3614b2a333278db9a340b0b059328649725e9e89f3eab
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An ACL 2025 long paper proposing ToolMaker, an agentic framework that autonomously turns a scientific paper's public code repository into an LLM-compatible tool, and TM-Bench, a 15-task benchmark for evaluating such tool creation."
  author: ["Georg Wölflein", "Dyke Ferber", "Daniel Truhn", "Ognjen Arandjelović", "Jakob N. Kather"]
  keywords: ["[[DefinedTerm/tool-creation]]"]
---

This paper starts from a limitation of LLM agents: the tools they call must be implemented in advance by human developers, which holds agents back in fields such as the life sciences and medicine that need large numbers of highly specialised tools. Noting that more and more scientific studies are published together with a public code repository, the authors ask whether an agent can autonomously download, install and wrap such existing code, so that researchers without the technical skills to deploy it could still use it.

Their answer is [[SoftwareApplication/toolmaker]]. Given a short task description, the URL of the paper's GitHub repository and a list of input arguments with example values, it installs the repository and its dependencies inside a Docker container and writes a Python function that performs the task, debugging that function through a closed-loop self-correction cycle. To evaluate it the paper introduces [[Dataset/tm-bench]], 15 computational tasks drawn mostly from pathology, radiology and omics, checked with held-out unit tests. ToolMaker correctly implements 12 of the 15 tasks, against 3 of 15 for [[SoftwareApplication/openhands]], the software-engineering agent the authors adapt as a baseline.

The paper was published in the Proceedings of the 63rd Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers), and its code and benchmark are public in the KatherLab/ToolMaker repository on GitHub.

## Key Points

- It frames [[DefinedTerm/tool-creation]] — letting LLMs create their own tools to expand their capabilities at runtime — as distinct from tool learning, which teaches LLMs to use human-crafted tools more effectively.
- It argues earlier tool-creation methods (it names CRAFT, CREATOR and LATM) can only produce simple, narrowly scoped tools, because they build each tool from scratch and cannot interact with the operating system; ToolMaker is presented as addressing both limitations.
- ToolMaker's workflow has two stages: environment setup, which produces a reproducible snapshot of the system as a Docker image, and tool implementation, which produces the Python function.
- During environment setup every write action the installing agent performs is recorded; because each can be expressed as a bash command, concatenating them yields the environment definition as a bash script or Dockerfile.
- In the self-correction loop the execution environment is reset to the freshly installed state before each run of the candidate tool, and the conversation history is restored to an earlier snapshot rather than accumulating every attempt, with summaries of all past attempts and the current code added on top.
- ToolMaker correctly implements 12 of 15 TM-Bench tasks (80%); the adapted OpenHands baseline, run with gpt-4o, correctly implements 3 of 15 (20%). A tool counts as correct only if every unit test of every held-out test invocation passes.
- The authors attribute most of OpenHands' failures to environment setup: nearly half of its environment definitions were invalid, and it often wrote installation scripts without testing them or omitted setup commands it had run manually.
- ToolMaker is more expensive per tool: on average 21.8 actions and $0.94, against 7.5 actions and $0.15 for OpenHands. The three tasks OpenHands solved were among the cheapest for ToolMaker, which the authors read as OpenHands handling only very easy tools.
- In the multi-step stamp_train_classification_model task, the self-correcting loop let ToolMaker discover that it had to extract features before training a classifier; that task took 9 iterations and 33 actions.
- Its tool for the esm_fold_predict task (predicting a protein's contact map from its sequence) was partially correct, passing two of three test invocations; the failed invocation contained a mask token that the example invocation lacked, and with such a token added to the example, the re-run tool passed every test invocation. The authors conclude the example invocation must be representative of the task.
- Adding task-specific paper summaries to the prompts did not raise either system's accuracy, but it reduced the number of actions and, for ToolMaker, of self-correcting iterations.
- Using o3-mini instead of gpt-4o lowered cost and degraded performance for both systems, and running OpenHands with Claude 3.5 Sonnet performed worse than with gpt-4o.

## Notes

The authors list several limitations. The framework assumes a reasonably well-structured, up-to-date and documented repository, and there is no guarantee that a given repository can be installed and used as a tool at all; the TM-Bench tasks were curated so that the authors could install and use each repository themselves. Passing the benchmark's unit tests does not guarantee correctness in every real-world scenario, and high-stakes uses such as clinical research would need further validation by domain experts. Although TM-Bench pins exact repository commits, repository deletion, force-pushes or renamed branches could still affect reproducibility. The paper also cautions that autonomously implementing complex biochemical tools could be misused, and that fully automated research systems need safety measures and ethical guidelines alongside technical capability.
