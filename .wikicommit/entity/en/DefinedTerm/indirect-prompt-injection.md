---
title: "indirect prompt injection"
type: "schema:DefinedTerm"
lang: en
tags: [mcp, security, terminology]
sources:
  - type: url
    url: 'https://developer.microsoft.com/blog/protecting-against-indirect-injection-attacks-mcp/'
    hash: sha256:75eb803ce303bb04ab925d41277a47055f64ccef01e15cfc3d3a0ed89110bbe6
  - type: url
    url: 'https://owasp.org/www-community/attacks/MCP_Tool_Poisoning'
    hash: sha256:6289aedc909fd48d101be69001b23cb0ccf12d0c5210c784f230f6ff154dc564
  - type: url
    url: 'https://www.coalitionforsecureai.org/wp-content/uploads/2026/03/model-context-protocol-security-1.pdf'
    hash: sha256:d5ea586dbd65785c34ba7afa769d56a4d1bcc77eb7876b7578edff5516c979a5
  - type: url
    url: 'https://arxiv.org/pdf/2606.22528'
    hash: sha256:ef37298f918eb3603bb29e729bf5490c27887bfadf9b5c6794e31dee79647cc2
  - type: url
    url: 'https://www.anthropic.com/engineering/managed-agents'
    hash: sha256:0e4e8bf6d9cb724da07f95297d00f7077a224890c85346851d0d455eba93d529
  - type: url
    url: 'https://www.sonarsource.com/state-of-code-developer-survey-report.pdf'
    hash: sha256:3d43f704cf1e52ecf4045d4342479248b68f557da49a051f79fb79b036967a0d
review_status: pending
generated_at: "2026-08-21"
generated_by: "claude-opus-5[1m]"

properties:
  description: "A security exploit against generative AI systems in which malicious instructions are embedded in external content the system later processes — documents, web pages, emails, or tool responses — and are then misread as valid user commands. Microsoft's guidance also calls it cross-domain prompt injection or XPIA, and treats tool poisoning as a subset of it."
---

Indirect prompt injection is, in Microsoft's formulation, "a security exploit targeting generative AI systems where malicious instructions are embedded in external content, such as documents, web pages, or emails." When the AI system processes that external content it misinterprets the embedded instructions as valid commands from the user, leading to unintended actions — data exfiltration, generation of harmful or misleading content, or manipulation of subsequent user interactions. Microsoft notes two further names for it, cross-domain prompt injection and XPIA, and presents it as the class of which [[DefinedTerm/tool-poisoning]] is a subset. The distinguishing feature against direct prompt injection is the delivery path: the instructions arrive inside content the system was asked to read, not inside the user's own prompt.

## Usage

The class became prominent as a concern for [[DefinedTerm/model-context-protocol]] deployments. Microsoft's own framing is that these vulnerabilities "are not new in the industry", but that their applicability to MCP and AI-based workloads warrants a closer look, since a malicious MCP server can expose customer data in ways organizations do not expect. OWASP's account of the MCP case locates the root cause in a trust gap between connect time and runtime: tool descriptions are reviewed once, when the agent first connects to a server, whereas tool responses go straight into the LLM context with no equivalent check — and that unguarded runtime channel is what an attacker abuses.

Microsoft recommends two lines of defence. The first is AI Prompt Shields, which it describes as a Microsoft-developed solution against both direct and indirect injection, working through machine-learning detection and filtering of malicious instructions in external content; **spotlighting**, which transforms the input text so the model can better distinguish valid system instructions from untrustworthy external input; **delimiters and datamarking**, where delimiters in the system message outline where input text begins and special markers highlight the boundaries of trusted and untrusted data; and continuous monitoring and updating of the shields themselves. The second is supply chain security: the security principles do not change in the AI era, but what counts as the supply chain now extends to foundation models, embeddings services and context providers, all requiring the same verification as traditional dependencies.

Microsoft closes on a fundamentals argument: that any AI implementation inherits the existing security posture of the organization's environment, so improving overall organizational posture comes first, and that on its reading of security research, getting the fundamentals right — enabling MFA, applying least privilege, keeping devices, infrastructure and applications up to date, and otherwise protecting important data — is the most effective protection against breaches of any kind.

The CoSAI threat model — set out in a report approved on 8 January 2026 but still marked "Status: Draft" — treats the underlying problem as structural rather than incidental. It proposes "Data/Control Boundary Distinction Failure" as its own threat category (MCP-T4), grouping tool poisoning, full schema poisoning and resource content poisoning as MCP-specific instances alongside prompt injection as an MCP-contextualized one, and names input sanitization, guardrails and context isolation as the controls. Its stated reason for needing a different threat model at all is that existing frameworks assume components behave predictably according to predefined logic, whereas, in its words, "MCP places an LLM, an agent whose behavior is shaped by natural language input, at the center of security-critical decisions, requiring a fundamentally different threat model."

### Injection that deletes rather than inserts

[[ScholarlyArticle/governance-decay]] describes a variant it calls the **Compaction-Eviction Attack**, which inverts the usual shape of the technique. Rather than smuggling an instruction *into* the agent's context, an adversary who can supply only in-context data biases the harness's [[DefinedTerm/compaction]] step into omitting a constraint the operator legitimately put there — removing a rule instead of adding one. The paper reports that optimizing the injection defeated every model it tested, including one that had been immune to its fixed probe, taking that model's violation rate from 0% to 65%.

The reason this matters beyond its novelty is what it targets. That paper's argument is that the runtime-enforcement defences proposed against ordinary injection — least-privilege tool authorization, policy monitors and DSLs, checks on execution paths — all "share an implicit assumption that the constraint is present at decision time," so an attack on the context-management layer undercuts them without engaging them. See [[DefinedTerm/governance-decay]] for the non-adversarial version of the same failure.

### Removing the credential from reach rather than narrowing it

[[TechArticle/scaling-managed-agents]] describes how an early architecture made injection cheap. With session, harness and sandbox in one container, any untrusted code Claude generated ran alongside the credentials, so "a prompt injection only had to convince Claude to read its own environment." The escalation path it names is what makes that severe: once an attacker holds those tokens, they can spawn fresh, unrestricted sessions and delegate work to them.

Its argument against the obvious mitigation is worth recording. Narrowly scoping the token, it says, "encodes an assumption about what Claude can't do with a limited token — and Claude is getting increasingly smart." The structural fix it adopts instead is that tokens are never reachable from the sandbox where generated code runs. Authentication is either bundled with the resource or held in a vault outside the sandbox: a repository access token clones the repo during sandbox initialisation and is wired into the local git remote, so push and pull work from inside without the agent ever handling the token; and OAuth credentials for custom tools sit in a vault reached through a dedicated MCP proxy, which exchanges a session-associated token for the real credential. The harness itself is never made aware of any credentials.

### How widely practitioners rate the risk

[[Report/state-of-code-developer-survey-2026]] measures concern about injection directly, and finds it stratified by organisation size rather than uniform. Enterprise developers are significantly more concerned than those at small and medium businesses about both direct prompt injections (34% against 25%) and indirect prompt injections (35% against 25%) — a gap that tracks the same report's finding on compliance with coding standards (38% against 28%). Every figure is that vendor's own survey of developers who use AI tools, not a measurement of incidence.

## Related Terms

[[DefinedTerm/tool-poisoning]] is the MCP-specific subset, though the sources disagree on where its payload sits: Microsoft and the CoSAI draft locate the injected instructions in tool descriptions and metadata, while OWASP locates them in tool responses at runtime. [[Report/model-context-protocol-security]] is that draft's fuller threat taxonomy, and [[TechArticle/protecting-against-indirect-prompt-injection-attacks-in-mcp]] is the Microsoft guidance summarised above. The protocol these attacks target is [[DefinedTerm/model-context-protocol]].
