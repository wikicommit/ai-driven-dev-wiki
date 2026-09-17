---
title: "AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses for LLM Agents"
type: "schema:ScholarlyArticle"
lang: en
tags: []
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2406.13352'
    hash: sha256:2c9c613f09075c0bfe05bf53bbf1993749267f8bf72bff9ba1f5651d007d1fff
review_status: pending
generated_at: "2026-09-16"
generated_by: "claude-sonnet-5"
generated_with: "0.6.1"

properties:
  description: "A NeurIPS 2024 paper introducing AgentDojo, an extensible benchmark environment populated with 97 realistic tasks and 629 security test cases, used to evaluate the utility and prompt-injection robustness of tool-calling LLM agents against a range of attacks and defenses."
  author: ["Edoardo Debenedetti", "Jie Zhang", "Mislav Balunovic", "Luca Beurer-Kellner", "Marc Fischer", "Florian Tramèr"]
  keywords: ["AgentDojo", "prompt injection", "AI agents", "benchmark", "tool calling"]
---

This paper introduces [[Dataset/agentdojo]], a dynamic benchmark environment for evaluating both the utility and the prompt-injection robustness of tool-calling AI agents, populated with four task suites (Workspace, Slack, Travel, and Banking) totaling 97 user tasks, 27 injection tasks, and 629 security test cases. Unlike a static benchmark with fixed attacks, the authors designed it to be extended with new environments, attacks, and defenses over time.

The paper evaluates a range of closed-source (Gemini 1.5 Flash and Pro, Claude 3 Sonnet and Opus, Claude 3.5 Sonnet, GPT-3.5 Turbo, GPT-4 Turbo, GPT-4o) and open-source (Llama 3 70B, Command R+) tool-calling agents on this benchmark, both without any attack present and under several prompt injection attacks and defenses.

## Key Points

- The paper finds that more capable models tend to be easier to attack, describing this as a form of inverse scaling, and reports that most models lose 10-25% of absolute utility once an attack is present.
- Attack success varies substantially by task suite: the paper reports a 92% attack success rate on the Slack suite (where attackers control a large fraction of tool outputs, e.g. via injected web page content), while one Travel-suite injection task requiring two unrelated malicious sub-goals succeeds 0% of the time.
- The paper's own "Important message" prompt injection — which directly addresses the model by name and uses the victim's real name — outperformed three prior attack phrasings it compared against (an "ignore previous instructions" attack, the InjecAgent attack, and a bare "TODO: {task}" instruction), and an adaptive attack that picks whichever of these four performs best per task ("Max") boosted the success rate further still.
- The paper reports that placing the injected instruction near the end of a tool's response message was the most effective injection position, reaching up to a 70% average success rate against GPT-4o.
- Knowing the victim's name and the target model's name gave the attack a small additional boost (the paper reports +1.9% for correctly guessing both), but the paper found that guessing either name incorrectly weakened the attack considerably (by roughly 22 percentage points in the paper's ablation).
- Of the four defenses evaluated against GPT-4o (data delimiting, a BERT-based prompt-injection detector, prompt/instruction repetition after each tool call, and a tool-filtering mechanism that restricts the agent to only the tools needed for a task before it sees untrusted data), the paper reports tool filtering was the most effective, lowering the targeted attack success rate to 7.5%; the paper notes several of the defenses actually increased benign utility, while the prompt-injection detector produced enough false positives to significantly degrade utility.
- The paper states that tool filtering fails when the required tool list cannot be planned in advance, or when the tools needed to solve the user's task are also sufficient to carry out the attack — a condition the paper says holds for 17% of its test cases — and that all evaluated defenses lost 15-20% of utility under attack.
- The paper's conclusion states that AgentDojo poses a challenge for both attackers and defenders: state-of-the-art LLMs fail at many of its tasks even without any attack present, and existing prompt injection attacks break some but not all of the security properties the benchmark tests.

## Notes

Several figures/tables in the extracted text are visually garbled by OCR/markdown conversion; the figures reported above are drawn from surrounding prose sentences that state them in readable form, not from the garbled table layouts themselves.
