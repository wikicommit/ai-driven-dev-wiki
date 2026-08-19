---
title: "tool poisoning"
type: "schema:DefinedTerm"
lang: en
tags: [mcp, security, terminology]
sources:
  - type: url
    url: 'https://owasp.org/www-community/attacks/MCP_Tool_Poisoning'
    hash: sha256:6289aedc909fd48d101be69001b23cb0ccf12d0c5210c784f230f6ff154dc564
  - type: url
    url: 'https://developer.microsoft.com/blog/protecting-against-indirect-injection-attacks-mcp/'
    hash: sha256:75eb803ce303bb04ab925d41277a47055f64ccef01e15cfc3d3a0ed89110bbe6
  - type: url
    url: 'https://www.coalitionforsecureai.org/wp-content/uploads/2026/03/model-context-protocol-security-1.pdf'
    hash: sha256:d5ea586dbd65785c34ba7afa769d56a4d1bcc77eb7876b7578edff5516c979a5
  - type: url
    url: 'https://arxiv.org/pdf/2503.23278'
    hash: sha256:e52e1f7bad32e6035ad5681f8775fce15eb345973f746db48783914ded82c6ab
  - type: url
    url: 'https://arxiv.org/pdf/2512.08290'
    hash: sha256:41c224d999eee798d882744ca794c7590e437175f2cbba1d8a6ca07317125f28
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "An attack on AI agents connected to Model Context Protocol servers in which hidden instructions are planted in a tool's metadata or in its responses, then treated by the LLM as trusted input. Sources differ on where the poison sits: Microsoft locates it in tool descriptions, OWASP in tool responses at runtime."
---

Tool poisoning is an attack against AI agents that reach external capabilities through [[DefinedTerm/model-context-protocol]] servers, in which an attacker plants instructions the LLM will read and follow as though they came from the user. Both accounts here treat it as a form of [[DefinedTerm/indirect-prompt-injection]], but they locate the poison in different places, and the difference matters for where a defence has to sit.

Microsoft describes tool poisoning as "a vulnerability where an attacker embeds malicious instructions within the descriptions of MCP tools." Every tool on a server carries metadata such as a name and a description, and LLMs use that metadata to decide which tools to invoke; compromised descriptions can therefore manipulate the model into unintended tool calls that bypass the controls meant to protect the system. Because the instructions live in metadata they are invisible to users while remaining legible to the model. Microsoft flags hosted servers as the sharpest case, since tool definitions can be amended after the fact to add malicious content — a manoeuvre it reports some researchers calling a "rug pull" — so a user who previously approved a tool can end up with a tool that has changed since that approval and can now perform undeclared actions.

OWASP's account, published under the title *MCP Tool Poisoning* and credited to the author kOaDT, moves the poison to runtime. There the attacker runs a malicious server whose "tools look normal, but their responses contain hidden instructions"; when the agent calls one, the injected instructions land in the context window and are treated as trusted input, and the model follows them — calling restricted tools, leaking data, or bypassing its own system prompt. Its stated root cause is a trust gap between connect time and runtime: descriptions are reviewed once, at connection, while responses go straight into context with no equivalent check.

## Usage

OWASP sets out the attack as a sequence: the attacker creates a server with normal-looking tool names and descriptions such as `get_compliance_status` or `fetch_user_data`; a victim connects an agent to it, whether through social engineering ("add this server for compliance checks") or because the server appears in a public registry; the agent calls a tool during normal operation; the server returns a response mixing real-looking data with embedded instructions, for example a fake compliance directive; the model treats the whole response as context and follows them; and the agent acts — calling a restricted tool, reading sensitive files, or sending data to an attacker-controlled endpoint. Its worked example is a server whose `get_compliance_status` tool returns a fabricated "COMPLIANCE DIRECTIVE" instructing the agent to read `/etc/shadow` and POST the contents to an external URL for "external validation".

The exposure OWASP identifies has three parts: applications that let users point an agent at arbitrary server URLs without restriction; agents that hold privileged tools such as file system, database or internal API access while also connecting to external servers; and client implementations that pass tool responses into context as-is. On that last point OWASP notes that the MCP specification treats server outputs as potentially untrusted and advises clients to consider trust boundaries, but does not mandate response validation before content reaches the LLM. Its named risk factors are unvalidated responses, internal and external tools sharing one privilege level, and system-prompt restrictions being enforced only by the model's instruction-following rather than by backend access controls.

Its prevention list is correspondingly structural: constrain response format toward structured output against a fixed schema and reject responses that do not match — while conceding that fully detecting injected instructions in free text is an open problem and schema validation only catches the obvious cases; isolate privileged tools in a separate agent context external servers cannot reach; enforce restrictions server-side at the tool execution layer rather than by prompt; maintain an allowlist of vetted servers; and require explicit user confirmation, obtained outside the LLM context, before destructive or data-exfiltrating actions.

The CoSAI threat taxonomy — proposed in a report approved on 8 January 2026 but still marked "Status: Draft" — lists Tool Poisoning as one of its seven Tier 1 MCP-specific threats, defining it as malicious modification of tool metadata, configuration or descriptors injected into clients via the `tools/list` method, and citing the specification's own statement that tool annotations should be considered untrusted unless obtained from a trusted server as making this "a recognized risk when clients connect to unvetted servers". That report also explicitly distinguishes two neighbouring threats from it: **Full Schema Poisoning**, which compromises the entire structural definition and type system of tools — hidden parameters, altered return types, malicious default values — rather than individual metadata; and **Resource Content Poisoning**, which hides instructions in the backend data sources a server retrieves rather than in tool definitions at all.

### In the academic taxonomies

Two surveys place the attack inside larger schemes, and both group it with neighbours worth naming.

[[ScholarlyArticle/mcp-landscape-security-threats]] locates tool poisoning under *capability declaration* by a **malicious developer** — one of four attacker types in its taxonomy — with the attack consequence recorded as a hidden malicious payload being executed. Its immediate neighbours in that group are **rug pulls**, whose consequence it gives as service disruption and loss of trust, and **cross-server shadowing**, where malicious functionality is hidden and lateral exploitation follows; alongside them sit namespace typosquatting, tool name conflict, preference manipulation and command injection. The same paper's reason for classifying by origin rather than by lifecycle phase is precisely this attack: tool poisoning and rug pulls "are introduced at the creation stage but triggered at operation".

[[ScholarlyArticle/sok-security-and-safety-in-the-mcp-ecosystem]] names tool masquerading and context poisoning as its examples of *adversarial security threats*, as against the *epistemic safety hazards* it treats as the other half of the problem, and groups rug pull attacks together with server impersonation and unauthorized tool mutation under supply-chain and model-switch attacks. It also lists tool poisoning among its index terms, and its wider argument bears directly on why this attack class is hard to contain: the coupling of context and action creates what it calls a "semantic attack surface", so a poisoned definition or response is not merely misleading output but a route to real-world operational damage.

## Related Terms

The parent class is [[DefinedTerm/indirect-prompt-injection]]; the protocol under attack is [[DefinedTerm/model-context-protocol]]. [[Report/model-context-protocol-security]] places the attack within that draft's twelve-category threat model, and [[TechArticle/protecting-against-indirect-prompt-injection-attacks-in-mcp]] is Microsoft's mitigation guidance.
