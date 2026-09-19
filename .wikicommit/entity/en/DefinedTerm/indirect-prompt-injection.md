---
title: "Indirect Prompt Injection"
type: "schema:DefinedTerm"
lang: en
tags: [agents, agent-safety, security, prompt-injection]
sources:
  - type: url
    url: 'https://arxiv.org/abs/2302.12173'
    hash: sha256:1e144027a6780c13f8ad053d161433e874416a09dfb69becbdb3ebfac34f9e31
  - type: url
    url: 'https://arxiv.org/pdf/2604.27202'
    hash: sha256:ec1b1d5a6010017bb19ec0c21ebfc834c928a2c0ba6c97cfaf109ffcef44937b
  - type: url
    url: 'https://arxiv.org/pdf/2606.28791'
    hash: sha256:0de559cacdfe9078d48a08a5f2b05d76219a579abd307e3a72ca17d1894464d0
  - type: url
    url: 'https://docs.anthropic.com/en/docs/test-and-evaluate/strengthen-guardrails/mitigate-jailbreaks'
    hash: sha256:cccb2171881ac7e3fdad07195764b42fff863153b2b262af3fd66a5ff5c7779c
  - type: url
    url: 'https://developer.nvidia.com/blog/mitigating-indirect-agents-md-injection-attacks-in-agentic-environments/'
    hash: sha256:12ff9c9af90eba6dbc268a3eab17b477eca5b0dc3c223d5537d795ba8b206089
  - type: url
    url: 'https://www.ibm.com/topics/prompt-injection'
    hash: sha256:a266835677476a694038cea4bd96f4ae88e318fe878bc7adcc4a28c90d8f3144
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A prompt-injection technique in which an attacker plants adversarial instructions in data an LLM-integrated application is likely to retrieve and process — rather than typing them into the model directly — letting the attacker remotely exploit the application without any direct interface to it."
---

Indirect prompt injection is a technique whose attack vectors were revealed by Greshake et al. in [[ScholarlyArticle/not-what-youve-signed-up-for]], for remotely exploiting an LLM-integrated application by strategically planting adversarial prompts in data the application is likely to retrieve — rather than an attacker needing to directly prompt the model themselves. It exploits the fact that LLM-integrated applications blur the line between data and instructions, so content the application merely retrieves and feeds to the model as context can act on the model the same way a direct instruction would.

## Usage

Beyond the adversarial framing that study introduced it under, the same mechanism has been put to defensive use. [[ScholarlyArticle/indirect-prompt-injection-in-the-wild]], a measurement study of 1.2 billion URLs, finds that instructions embedded in web pages pursue six distinct objectives spanning offensive, defensive and underspecified uses. On the offensive side the study records system disruption — instructing an agent to emit random strings, repeated nonsense or text intended to exhaust context limits — along with reputation manipulation through content promotion, citation forcing and positive-review forcing, and a small number of data-exfiltration attempts. On the defensive side it records site owners asserting copyright and personal-data restrictions against automated reuse, and an AI-bot-identification pattern in which a page asks any reading model to include a marker phrase in its response so that automated visitors can be detected. Its authors read this as a multi-stakeholder ecosystem with competing incentives rather than a purely malicious practice, and characterize current deployment as working more through friction and degradation than through reliable control.

That study also reports how such instructions are delivered in practice. Task override — directly replacing the model's current instructions rather than persuading it — appears in 99% of the instances it validated, often reinforced by jailbreak-style framing. Most are not meant for human eyes: about 70% sit in channels that are never rendered, such as HTTP response headers, comments, structured data and metadata fields, and among those embedded in rendered HTML the great majority are concealed by techniques such as colour and contrast manipulation, occlusion and viewport-based hiding. The instructions are also highly templated, with 54 lexical templates accounting for 95% of cases, and durable: 65% of the affected pages already carried an injection twelve months before the snapshot analysed.

## When It Applies

It applies to LLM-integrated applications that retrieve data likely to contain adversarial content and pass it to the model as part of its context, without the application separating retrieved data from instructions. The paper that introduced the technique demonstrated its practical viability against real-world systems, including Bing's GPT-4-powered Chat and code-completion engines, and against synthetic applications built on GPT-4, showing that a retrieved, injected prompt can act as arbitrary code execution from the application's perspective and can manipulate whether and how the application calls other APIs. The introducing paper states that effective mitigations against this class of attack were lacking at the time of writing.

How much it succeeds depends heavily on how the retrieved content is presented to the model. In 5,200 controlled trials across 13 models and four page representations, the measurement study found compliance limited but non-negligible, peaking at 8% for small models on plain text and falling to between 0.2% and 1.1% where structural cues were preserved — its explanation being that flattening a page strips away the markup, comments, metadata and styling that would otherwise reveal an instruction as hidden and out of place. Two cautions attach to that result. Lower compliance on richer representations is not the same as robustness, because those representations are much longer and frequently caused models to fail before producing usable output at all. And recognizing an injection is not the same as resisting it: the study records cases in which a model explicitly warned about the injected instruction and complied with it anyway.

Its authors present their figures as a lower bound, since their corpus draws mainly on public web crawls that may underrepresent authenticated content and their detection relies on an indicator list that may miss obfuscated or non-English variants. They also note that the instructions they observed are overwhelmingly static strings, and caution against reading today's modest effectiveness as a long-term ceiling.

A third source approaches the same class from the agent-security side.
[[ScholarlyArticle/from-determinism-to-delegation]] treats indirect prompt injection as the case where
the risk of agentic systems is amplified by agency itself: a poisoned document or web page can induce
an agent to misuse a legitimate tool — its example is exfiltrating data through an email capability.
Citing a tool-integrated benchmark, it reports ReAct-prompted GPT-4 agents being successfully attacked
in roughly 24% of cases — a tool-integrated agent benchmark, so not directly comparable with the
webpage-summarization compliance rates above. The defences it names differ in kind from classical perimeter security: strict
tool-permission scoping, output guardrails, sandboxed execution, and human-in-the-loop checkpoints for
destructive actions. It lists security under agency among its open problems, describing the defences as
immature and calling for further formalization of provenance, capability scoping and verifiable
guardrails.

A fourth account comes from the vendor side. Anthropic's platform documentation treats indirect
prompt injection as one of two threat models an application must defend against, and defines it by
who the adversary is: the user is trusted, and it is the *third-party content* the model reads on
that user's behalf — the body of an inbound email, a fetched web page, OCR output from an uploaded
file, the result of a tool call — that an attacker may have influenced. It sets this against
jailbreaks and direct prompt injection, where the application's own user is the adversary (see
[[DefinedTerm/jailbreaking]]).

The mitigations it gives follow from structuring the application so the model can reliably tell
untrusted content from the application's own instructions. Third-party content should be delivered
only inside `tool_result` blocks and never in system prompts or plain user text blocks, on the
stated grounds that Claude is trained to treat instructions appearing inside tool results with
appropriate skepticism; the tool's description or the result's structure should say what the
content is and where it came from, so the model can calibrate how much to trust any embedded
directives; and the system prompt should state outright that tool, document and search results are
untrusted data that must never override it or the user's request. It recommends JSON-encoding
untrusted strings rather than concatenating them into free-form text, since JSON escaping gives
unambiguous delimiters an attacker cannot close a quote or tag to break out of. The converse also
holds on that account: because tool-result content is treated as untrusted, a developer's own
instructions placed there may be ignored or flagged, and belong in a following user turn instead.
Beyond the message structure it names least privilege over the data and actions the model can
reach, screening each tool's raw output through a small classifier before returning it, and
red-teaming the workflow with documents and tool outputs that deliberately contain injection
attempts. It also states that Anthropic runs additional classifiers over what the computer use and
browser use tools return, scanning screenshots and page text for potential injections and steering
Claude to check whether an instruction really came from the user before acting.

A fifth account narrows the vector to a coding agent's own configuration files. An NVIDIA AI Red Team report describes a malicious dependency writing an [[DefinedTerm/agents-md]] file during a build, so that instructions reach the agent with the standing of project configuration rather than as retrieved content. What distinguishes this case from the retrieved-document form above is where the injected text sits in the agent's trust model: an instruction file is something the agent is built to obey, so the attack needs no concealment from the model and instead concealed itself from the human reviewer, chaining a second injection through a source comment addressed to the model that would summarize the pull request. Its precondition is correspondingly stronger — the attacker must already have code execution in the build environment — and the affected vendor concluded on that basis that it did not materially raise risk beyond a compromised dependency. See [[DefinedTerm/indirect-agents-md-injection]].

A sixth account, a general IBM explainer on prompt injection, adds two things to the picture above
rather than restating it. It contributes a non-textual vector — noting that malicious prompts do not
have to be written in plain text and can be embedded in images the model scans — and a worked chain
in which the injected instruction propagates: researchers are reported to have designed a worm
spreading through AI-powered virtual assistants, in which a malicious prompt arrives by email,
induces the assistant asked to summarize it to send sensitive data to the attackers, and further
directs the assistant to forward the malicious prompt to other contacts. Its own framing example is
the simpler retrieved-content case, an attacker posting a prompt to a forum telling models to direct
their users to a phishing site, so that an assistant asked to summarize the discussion relays that
instruction to an unsuspecting user. That source classifies the technique as one of two types of
prompt injection, against [[DefinedTerm/direct-prompt-injection]].

## Related Terms

[[ScholarlyArticle/not-what-youve-signed-up-for]], [[ScholarlyArticle/indirect-prompt-injection-in-the-wild]], [[DefinedTerm/two-channel-prompt-injection]], [[DefinedTerm/tool-poisoning]], [[DefinedTerm/indirect-agents-md-injection]], [[DefinedTerm/guardrails]], [[DefinedTerm/jailbreaking]]

- [[ScholarlyArticle/from-determinism-to-delegation]] — source of the measured tool-integrated attack
  rate and the agent-side defences above
- [[DefinedTerm/supervised-agency-spectrum]] — the graduated-oversight framing those defences sit in
- [[DefinedTerm/direct-prompt-injection]] — the other of the two types the sixth account divides the attack into
