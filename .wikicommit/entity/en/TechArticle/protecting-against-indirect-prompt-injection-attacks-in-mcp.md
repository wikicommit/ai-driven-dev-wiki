---
title: "Protecting against indirect prompt injection attacks in MCP"
type: "schema:TechArticle"
lang: en
tags: [mcp, security]
sources:
  - type: url
    url: 'https://developer.microsoft.com/blog/protecting-against-indirect-injection-attacks-mcp/'
    hash: sha256:75eb803ce303bb04ab925d41277a47055f64ccef01e15cfc3d3a0ed89110bbe6
review_status: pending
generated_at: "2026-08-19"
generated_by: "claude-opus-5[1m]"

properties:
  description: "Microsoft developer-blog guidance of 28 April 2025 on mitigating prompt injection in Model Context Protocol deployments, recommending AI Prompt Shields and supply chain security, and defining indirect prompt injection and tool poisoning for an MCP audience."
  author: ["Sarah Young", "Den Delimarsky"]
  datePublished: "2025-04-28"
  publisher: "Microsoft"
---

"Protecting against indirect prompt injection attacks in MCP" is a post of 28 April 2025 on Microsoft's developer blog by Sarah Young, a Principal Security Advocate at Microsoft, and Den Delimarsky, a Principal Product Engineer. It sets out guidelines for mitigating prompt injection in [[DefinedTerm/model-context-protocol]] deployments and describes the steps Microsoft has taken to address the risk for its customers.

Its framing of MCP is developer-facing rather than protocol-facing: MCP is described as an open protocol spearheaded by Anthropic that provides a consistent API contract for passing context between applications and LLMs, structured methods for tool calling and data retrieval, and a common format for LLM inputs and outputs — solving, from an implementation perspective, the need to rewrite integration code when switching model providers or updating context-fetching functions, reducing boilerplate and separating application logic from the AI reasoning layer.

## Key Practices

- **Recognise the attack class.** The post defines [[DefinedTerm/indirect-prompt-injection]] — also called cross-domain prompt injection or XPIA — as malicious instructions embedded in external content such as documents, web pages or emails, which the AI system misinterprets as valid user commands, leading to data exfiltration, harmful or misleading output, or manipulation of later interactions.
- **Treat [[DefinedTerm/tool-poisoning]] as a subset of it.** Here the malicious instructions live in the descriptions of MCP tools; because LLMs use that metadata to decide which tools to invoke, compromised descriptions can drive unintended tool calls that bypass security controls, while remaining invisible to the user. The post flags hosted servers as the sharper case, where definitions can be amended after approval to add malicious content — a manoeuvre it says some researchers call a "rug pull" — leaving a previously approved tool able to perform undeclared actions.
- **Deploy AI Prompt Shields.** Described as a Microsoft solution against both direct and indirect injection, working through four mechanisms: machine-learning detection and filtering of malicious instructions in external content; **spotlighting**, transforming input text so the model can better distinguish valid system instructions from untrustworthy external input; **delimiters and datamarking**, using delimiters in the system message to mark where input text sits and special markers to bound trusted versus untrusted data; and continuous monitoring and updating of the shields against new techniques.
- **Extend supply chain security to AI components.** The post argues the security principles do not change, only what counts as the supply chain: it now includes foundation models, embeddings services and context providers, which need the same rigorous verification as traditional dependencies. It points to GitHub Advanced Security's secret, dependency and CodeQL scanning, integrated into Azure DevOps and Azure Repos, and notes Microsoft applies these practices internally.
- **Get the fundamentals right first.** Any AI implementation inherits the existing security posture of the organization's environment, so improving overall posture is recommended before anything AI-specific. On its own reading of security research, the practices that matter most are enabling MFA, applying least privilege, keeping devices, infrastructure and applications up to date, and otherwise protecting important data — which it presents as the most effective protection against breaches of any kind.

## Scope & Caveats

The post is guidance rather than a threat taxonomy: it names two attack classes and two mitigation strategies, and does not enumerate MCP threats systematically — for that see [[Report/model-context-protocol-security]]. It is also vendor-situated, and says so implicitly by recommending Microsoft's own Prompt Shields, GitHub Advanced Security and Azure AI Foundry built-in platform protection as the path to using AI and AI agents safely. Its own hedge on the underlying premise is that these vulnerabilities "are not new in the industry", but that their applicability to MCP and AI-based workloads warrants a closer look; and it concedes that using AI potentially increases an application's attack surface.
