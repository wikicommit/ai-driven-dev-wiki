---
title: "Guardrails"
type: "schema:DefinedTerm"
lang: en
tags: [agents, agent-safety, security]
sources:
  - type: url
    url: 'https://about.gitlab.com/the-source/ai/implementing-effective-guardrails-for-ai-agents'
    hash: sha256:fec4dd1d58e4a51a864185fa402e79f338ebea7e0e5f125356978be821500ca8
  - type: url
    url: 'https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf'
    hash: sha256:9d619ed7dd7cb94569658ca3de72615ef792761e6e4147e36c45edf2f945bbf9
  - type: url
    url: 'https://dev.to/aws/ai-agent-guardrails-rules-that-llms-cannot-bypass-596d'
    hash: sha256:d321340a9dfb2556bc45605cd43311d6f886dd3c139f618c6380e18345aa7a1a
review_status: pending
generated_at: "2026-09-19"
generated_by: "claude-opus-5[1m]"
generated_with: "0.6.1"

properties:
  description: "A term used at three different layers for the controls placed around an AI agent — organizational access controls, approval gates and audit trails; application-level classifiers screening what reaches and leaves the model; and deterministic framework-level rules evaluated before a tool call runs. The sources here do not share one definition, and none of the three is the agreed one."
---

Guardrails are the policies, controls and mechanisms placed around an AI agent to constrain what it is permitted to do. The word is used at several layers and the sources here do not share one definition of it, so no single formulation below should be read as the agreed one.

One account, set out in [[BlogPosting/implementing-effective-guardrails-for-ai-agents]], is organizational and specific to software delivery: on it, guardrails are a comprehensive framework of policies, controls, and monitoring mechanisms that govern how AI agents interact with a development environment, and the concept is described there as extending beyond traditional security controls — ensuring AI systems operate safely and effectively while complying with organizational policies and regulatory requirements, as agents take on sensitive operations such as autonomous code generation and automated infrastructure management that traditionally required human oversight.

That is the first of three accounts, and they approach the word from different ends and are worth keeping apart. The first is organizational, describing the access controls, approval gates and audit trails an enterprise places around an agent's actions. A second is application-level, describing the classifiers and filters a developer places around an agent's inputs and outputs. A third is framework-level and deterministic, placing rules in code that runs outside the model and decides whether a tool call may execute at all. All use the same word for the same purpose — constraining what an agent can do — but they operate at different layers and none subsumes the others.

## Usage

Based on interviews with 54 DevSecOps practitioners and leaders, that first account groups guardrails for AI agents into four categories. User roles and access controls require two-factor authentication or single sign-on before granting an AI tool system access, plus role-based access control for AI operations touching secrets, credentials, or protected branches. Limits and controls constrain what an agent's actions can do directly: blocking direct production deployment without manual review, routing AI-generated changes through the same merge-request review process as human-authored changes, requiring manual approval above defined cost thresholds, applying multiple-review requirements to infrastructure or resource deletion, and maintaining rollback capability for all agent actions. Customization lets an organization adapt these boundaries to its own operational procedures: admin-configurable forbidden commands (e.g., erasing Terraform state, changing domain names), human touchpoints scaled to customer impact, and adjustable automation levels by user role. Logging, tracking, and transparency covers audit trails that capture both AI-initiated changes and the human approvals involved, explanations for AI decisions, licensing-compliance checks on AI-generated and third-party code, and granular, compliance-driven controls over production data access.

[[TechArticle/a-practical-guide-to-building-agents]] treats guardrails at the level of a single application, and as a layered defence rather than a single control: OpenAI's position there is that one guardrail is unlikely to provide sufficient protection, and that multiple specialized guardrails used together create more resilient agents. Its worked configuration combines LLM-based guardrails, rules-based protections such as regex, and a moderation API to vet user input before a function call proceeds. That guide names seven types:

- **Relevance classifier** — keeps responses within the intended scope by flagging off-topic queries.
- **Safety classifier** — detects jailbreak and prompt-injection attempts, its example being a request to role-play as a teacher reciting the system instructions.
- **PII filter** — vets model output for personally identifiable information.
- **Moderation** — flags hate speech, harassment and violence in inputs.
- **Tool safeguards** — rate each available tool low, medium or high risk on factors such as read-only versus write access, reversibility, required account permissions and financial impact, then use the rating to pause for checks before high-risk calls or escalate to a human.
- **Rules-based protections** — deterministic measures such as blocklists, input length limits and regex filters against known threats.
- **Output validation** — prompt engineering and content checks that keep responses aligned with brand values.

The same guide gives a three-step heuristic for building them: focus first on data privacy and content safety, add new guardrails as real-world edge cases and failures appear, and optimize for both security and user experience as the agent evolves. It also stresses that guardrails are not a substitute for ordinary security engineering, and should be coupled with robust authentication and authorization protocols, strict access controls, and standard software security measures. In [[SoftwareApplication/openai-agents-sdk]] this is realised as an `@input_guardrail` function whose `tripwire_triggered` output interrupts the run, with guardrails executing concurrently with the primary agent rather than ahead of it.

That guide's last guardrail is not a filter at all: it treats planning for [[DefinedTerm/human-in-the-loop]] intervention as a critical safeguard, naming two triggers — exceeding failure thresholds, and high-risk actions that are sensitive, irreversible or high-stakes.

A third account places guardrails lower still, in the agent framework itself rather than in a classifier or an organizational process. On this framing, described in [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]], a guardrail expressed as prose — in a system prompt or a tool's docstring — is input the model interprets and re-decides on every call, so it constrains nothing reliably; that post's example is an agent that confirms a booking without the payment its tool docstring requires, and reports success. The guardrail it proposes instead is a deterministic rule evaluated by a pre-execution interceptor, which cancels the call before the tool runs and returns the violation to the model as the result. What distinguishes this sense from the classifier-based one above is not the layer alone but the kind of decision: these rules are boolean predicates over a tool call's parameters rather than probabilistic judgements about content, and the post reports zero false positives and zero false negatives across its three demonstration scenarios. That determinism is bounded by what has been written down — the post states that a rule must be explicitly defined for each operation to be protected, so an operation nobody wrote a rule for is not covered. See [[DefinedTerm/neurosymbolic-validation]] for the pattern and [[DefinedTerm/agent-hooks]] for the interception mechanism it relies on.

## Related Terms

[[DefinedTerm/sandboxing]], [[DefinedTerm/human-in-the-loop]], [[DefinedTerm/agentic-engineering]], [[DefinedTerm/neurosymbolic-validation]], [[DefinedTerm/agent-hooks]], [[BlogPosting/implementing-effective-guardrails-for-ai-agents]], [[BlogPosting/ai-agent-guardrails-rules-that-llms-cannot-bypass]], [[TechArticle/a-practical-guide-to-building-agents]]
