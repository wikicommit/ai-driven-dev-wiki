---
title: "MCP-ITP: An Automated Framework for Implicit Tool Poisoning in MCP"
type: "schema:ScholarlyArticle"
lang: en
tags: [mcp, security, agents, prompt-injection]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2601.07395'
    hash: sha256:02a5d5f74b794c1e19fa444390d6ae855747ee58de6120b249b03b5680f40bfc
review_status: pending
generated_at: "2026-09-24"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "A security paper that proposes MCP-ITP, an automated black-box framework for generating implicitly poisoned MCP tools — tools whose descriptions redirect an agent into calling a different, legitimate but high-privilege tool — and evaluates it on the MCPTox dataset across 12 LLM agent settings."
  author: ["Ruiqi Li", "Zhiqiang Wang", "Yunhao Yao", "Xiang-Yang Li"]
  datePublished: "2026-01-12"
  abstract: "The paper focuses on implicit tool poisoning in the Model Context Protocol, where the poisoned tool itself is never invoked and its metadata instead induces the agent to call a legitimate high-privilege tool. It formulates poisoned-tool generation as a black-box optimization problem, iteratively refining tool descriptions with feedback from an evaluator LLM and a detector LLM to maximize attack success while evading detection."
---

This paper is about an attack on agents that use the [[DefinedTerm/model-context-protocol]] (MCP). In the [[DefinedTerm/tool-poisoning]] attacks it builds on, malicious instructions are embedded in a tool's metadata and loaded into the agent's context when the tool is registered. The authors characterize prior work as focused mainly on explicit tool poisoning — getting the agent to call the poisoned tool itself — or as relying on manually crafted poisoned tools, and argue that explicit attacks are exposed to detection because the agent has to visibly execute the suspicious tool. They instead study [[DefinedTerm/implicit-tool-poisoning]], in which the poisoned tool is never invoked at all: its description manipulates the agent's contextual reasoning so that it calls an existing, legitimate but high-privilege tool to perform the malicious operation, decoupling the trigger from the tool that is eventually called.

Their contribution, which they describe as the first automated and adaptive framework for implicit tool poisoning in the MCP ecosystem, is MCP-ITP. It treats the construction of a poisoned tool as a black-box optimization problem — the attacker sees neither users' real queries nor the agent's internals, but can inspect the tools a benign server exposes and publish its own tool through an attacker-controlled server. The poisoned description is split into two parts: a fixed camouflage part that makes the tool look functionally equivalent to a legitimate original tool, and an optimized part that carries the redirection. Three LLMs drive the optimization: an attacker model generates candidate descriptions, a detector model simulates LLM-based malicious-tool detection, and an evaluator model tests each candidate against a set of "shadow queries" that would normally trigger the original tool. Detector verdicts and evaluator outcomes are fed back into the next round of a tree-structured search.

The evaluation uses the MCPTox dataset — built on 45 real-world MCP servers and 353 real tools, with 1,497 malicious test cases — restricted to the 548 cases corresponding to implicit poisoning, and compares MCP-ITP against MCPTox's hand-crafted poisoned tools across 12 LLM agent settings drawn from the GPT, DeepSeek, Qwen and Gemini families. The authors conclude that implicit tool poisoning is a practical threat to the MCP ecosystem and that targeted defenses are urgently needed.

## Key Points

- In the reported setup, DeepSeek-V3 serves as the attacker model, Qwen3-32b as the evaluator and Qwen3-8b as the detector, with five candidates per round, a tree width of one and three iterations by default.
- MCP-ITP reaches higher attack success rate (ASR) than the MCPTox baseline in all 12 agent settings, and by more than 10 percentage points in 8 of them: on GPT-3.5-turbo from 48.2% to 84.2%, on DeepSeek-V3 from 44.8% to 78.4%, and on Qwen3-32b with reasoning enabled from 45.1% to 69.9%.
- The gains come mainly from fewer "Ignored" outcomes, where the agent is unaffected and calls the original tool: on o1-mini these fall from 19.9% to 4.2%, and on DeepSeek-V3 from 38.0% to 14.8%.
- MCP-ITP's poisoned tools are also harder to detect. Against the AI-Infra-Guard detector, the malicious-tool detection rate (MDR) on o1-mini drops from 17.22% for MCPTox's tools to 0.96%, and against an Oracle detector from 77.35% to 31.39%.
- Within the Qwen3 family, more capable models were more vulnerable, and enabling reasoning mode sharply increased ASR — for Qwen3-8b from 7.44% to 40.5%, and for Qwen3-32b from 28.8% to 69.9%. The authors relate this to the inverse-scaling phenomenon, suggesting greater capability can increase susceptibility to poisoned in-context tool specifications.
- Adding the camouflage part to the description raised ASR for higher-capability models (o1-mini by 2.6 points, GPT-4o-mini by 7.7, DeepSeek-R1 by 4.6) but lowered it for weaker models such as the Qwen3 models and Gemini-2.5-flash, for which the shorter description worked better.
- Using the weaker Qwen3-32b rather than o1-mini as the evaluator generally produced higher ASR and better cross-model generalization. The authors attribute this to a capable evaluator letting candidates meet the score threshold too early, stopping the search before it finds more robust manipulation patterns.

## Notes

The authors note two limitations: MDR still rises when stronger models are used in LLM-based detection, and the evaluation is restricted to MCPTox because datasets for MCP-specific implicit tool poisoning are still limited. The main results come from a single evaluation per setting. They state that the attacks were not deployed against real-world or live systems, that experiments were run in controlled environments, and that any personal data in the dataset is randomly generated.

The paper appears as arXiv:2601.07395v1 [cs.CR], dated 12 January 2026; all four authors are affiliated with the University of Science and Technology of China.
