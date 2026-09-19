---
title: "Securing LLM Systems Against Prompt Injection"
type: "schema:BlogPosting"
lang: en
tags: [llm, security, prompt-injection, tool-use]
sources:
  - type: url
    url: 'https://developer.nvidia.com/blog/securing-llm-systems-against-prompt-injection/'
    hash: sha256:3586be2459ba07a9385bba9fe13f4902a44075110ce0e0594535f80200bc5848
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A disclosure of three prompt-injection-reachable vulnerabilities in LangChain chains — remote code execution, server-side request forgery and SQL injection — used to argue that the control and data planes are not separable in an LLM prompt, so all model output must be treated as potentially attacker-controlled."
  author: "Rich Harang"
  publisher: "[[Organization/nvidia]]"
  datePublished: "2023-08-03"
---

The post explains prompt injection and then uses it against three [[SoftwareApplication/langchain]] chains the NVIDIA AI Red Team examined, to show what the technique buys an attacker once a model's output is wired into an external service. It is explicit that the vulnerabilities are in those chains rather than in LangChain's core engine or in the third-party APIs they reach.

Its account of the mechanism starts small. A prompt defining a shoe-shop chatbot is followed by whatever the customer types, so a customer who writes "IGNORE ALL PREVIOUS INSTRUCTIONS" followed by their own instructions can have the bot insult them instead — harmless in itself, and offered as the shape of the attack rather than its consequence. The consequence arrives when the model's output is not merely shown to a user but used to build a call to something else.

All three vulnerabilities share one structure: a chain turns user input into an LLM request, interprets the result into a call to an external service, and formats what comes back. An attacker who controls the model's output controls what the chain sends onward, and whatever authority that service grants the chain becomes reachable. The post's general conclusion is drawn from that structure rather than from the individual bugs — that control and data are not separable in a prompt, so every model production must be treated as potentially malicious and sanitized before anything further is done with it.

## Key Points

- Prompt injection is described as an attack technique specific to LLMs that lets an attacker manipulate the model's output, made more dangerous by plug-ins that let the model reach external services.
- The `llm_math` chain enabled remote code execution through its Python interpreter: phrased as an order rather than a maths problem, the model emits attacker-chosen code and the evaluation engine runs it. It is recorded as CVE-2023-29374 with a CVSS score of 9.8, and the specific exploit was fixed as of version 0.0.141.
- The `APIChain.from_llm_and_api_docs` chain enabled server-side request forgery — declaring a new query redirects the fetch to a different URL than the one in the system prompt. Recorded as CVE-2023-32786, reported exploitable up to and including version 0.0.193 at the time of writing.
- The `SQLDatabaseChain` enabled SQL injection through the same "ignore all previous instructions" framing. Recorded as CVE-2023-32785, also reported exploitable up to and including version 0.0.193.
- The stated root cause is that control and data planes are not separable when working with LLMs: a single prompt contains both, and injection inserts control where data is expected. The post treats this as why prompt injection attacks "cannot be effectively mitigated" rather than as a bug to be patched.
- Its primary recommendation is to treat every LLM production as potentially malicious and under the control of anyone who can get text into the model's input, inspecting and sanitizing it before parsing.
- It holds that external service calls must be strictly parameterized and made in a least-privileged context, with the lowest privilege level of any entity that contributed to the prompt applied to each subsequent call.
- It advises against connecting LLMs to external resources where reasonably avoidable, and singles out multistep chains calling several services as needing rigorous security review.
- It advises that plug-ins requiring authorization should generally not be used after other plug-ins have been called, on the stated grounds that cross-plug-in authorization is highly complex.
- All three exploits were performed against the OpenAI `text-davinci-003` API as the base model, and the post notes that other models would likely need slight prompt modifications.

## Context

The post is published on NVIDIA's technical blog and reports its own red team's findings. It sets out its reasoning for disclosing publicly: the vulnerabilities are potentially severe but confined to specific chains rather than core components, prompt injection is by then widely understood as an attack technique, and the affected components had been removed from the latest version. It records that the remote code execution issue was independently found by several parties, and that NVIDIA requested a CVE at the end of March 2023 after what it describes as a lack of immediate mitigation. It closes by thanking the LangChain team for their engagement and describes the exchange as a good example of handling coordinated disclosure in a new domain.
