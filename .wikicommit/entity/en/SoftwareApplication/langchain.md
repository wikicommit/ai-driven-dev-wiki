---
title: "LangChain"
type: "schema:SoftwareApplication"
lang: en
tags: [agents, agent-frameworks, llm, tool-use]
sources:
  - type: url
    url: 'https://developer.nvidia.com/blog/securing-llm-systems-against-prompt-injection/'
    hash: sha256:3586be2459ba07a9385bba9fe13f4902a44075110ce0e0594535f80200bc5848
  - type: url
    url: 'https://blog.langchain.com/agent-frameworks-runtimes-and-harnesses-oh-my/'
    hash: sha256:dbbb531bd6a1b614e8c6537f3fe67ea744c2f9b7a8532abd9bfc3cd413ce1729
  - type: url
    url: 'https://blog.langchain.com/agent-middleware'
    hash: sha256:071e79d936c9e2d2b07b0eab257fff6823cbeb8a320c72649b9ca211b9cd7179
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5[1m]"
generated_with: "0.7.0"

properties:
  description: "An open-source library providing tools for building applications on top of LLMs. It defines chains and agents that take user input, pass it to a model, and act on the result — including by calling third-party APIs. Its makers classify it as an agent framework, and version 1.0 introduced middleware as its agent abstraction."
  applicationCategory: "LLM application framework"
  featureList: "Chains and agents connecting LLM output to external tools and data; third-party API integration; a core library separate from the example chains built on it; agent middleware with before_model, after_model and modify_model_request hooks (1.0); abstractions for structured content blocks and the agent loop (1.0)"
---

LangChain is an open-source library offering a collection of tools for building flexible applications that use large language models. It defines "chains" — also called plug-ins — and "agents" which take user input, usually combine it with a developer-supplied prompt, pass it to a model, and then use the model's output to trigger further actions: looking something up online, searching a database, or constructing a program to solve a problem.

Part of the account here comes from a security analysis rather than from the project's own documentation, and part from LangChain's own blog. The security analysis draws a three-way distinction it says matters: the core library, which provides the tools for building chains and agents and connecting them to third-party APIs; the chains and agents built with it; and the third-party APIs and tools those reach.

## Capabilities

- Chains and agents act as an intermediary between user and model: a prompt template converts user input into an LLM request, the result is interpreted into a call to an external service, and a final step — often using the model again — formats what comes back.
- The library connects LLMs to external data sources and computation, which the analysis describes as providing tremendous power and flexibility to such applications.
- LangChain 1.0 introduced [[DefinedTerm/agent-middleware]] as its agent abstraction, announced in [[BlogPosting/agent-middleware]]. The core loop remains a model node and a tool node; middleware hooks in before the model call (`before_model`), after it (`after_model`), or by changing a single request's tools, prompt, messages, model, settings, output format and tool choice (`modify_model_request`), and several middleware run in order on the way in and in reverse on the way out. The team calls it the biggest new part of 1.0.
- The alpha shipped three middleware implementations — human-in-the-loop review of tool calls, summarization of long message histories, and Anthropic prompt caching — which the team says it already used in internal agents, and it states that middleware can replicate the supervisor, swarm, bigtool, deepagents and reflection architectures it had shipped as separate LangGraph agents.
- The same post places middleware at the end of a longer line of agent customization: LangChain had had agent abstractions for nearly three years, a version of the model-prompt-tools loop having existed in November 2022, and over the preceding two years it had added runtime configuration, custom state schemas, dynamic prompts, full control over the message list, pre- and post-model hooks and per-call model selection as agent parameters — an approach it says produced too many interdependent parameters to coordinate.

## Security History

The NVIDIA AI Red Team identified and verified three vulnerabilities in LangChain chains, all reachable through [[DefinedTerm/prompt-injection]] and all sharing the pattern above — the attacker controls the model's output, and so controls what the chain sends to the external service. The `llm_math` chain allowed remote code execution through its Python interpreter (CVE-2023-29374, CVSS 9.8), fixed as of version 0.0.141; `APIChain.from_llm_and_api_docs` allowed server-side request forgery (CVE-2023-32786) and `SQLDatabaseChain` allowed SQL injection (CVE-2023-32785), both reported still exploitable up to and including version 0.0.193 at the time of writing.

The analysis is explicit that these affect specific chains and not the core engine, describing the affected chains as provided largely as examples of the library's capabilities. It reports that the latest version at the time had removed them from the core library, that they remained importable from older versions, and it urged users to update. It records the first public disclosure as coming from a third party through a LangChain GitHub issue in January 2023, two further disclosures the following month, and NVIDIA requesting a CVE at the end of March 2023; the remaining two were disclosed in April 2023 and published with the LangChain team's approval. Its closing acknowledgement thanks that team for their engagement and describes the exchange as a good example of handling coordinated disclosure in a new domain.

## Adoption & Ecosystem

Harrison Chase, writing on LangChain's blog in [[BlogPosting/agent-frameworks-runtimes-and-harnesses]], classifies LangChain as an [[DefinedTerm/agent-framework]] — a package whose main value lies in its abstractions — as opposed to [[SoftwareApplication/langgraph]], which he calls an [[DefinedTerm/agent-runtime]], and [[SoftwareApplication/deep-agents]], an [[DefinedTerm/agent-harness]]. He names LangChain and LangGraph as the biggest of the open-source packages LangChain maintains, says LangChain 1.0 is built on top of LangGraph to use its runtime, and says the 1.0 work went into abstractions for structured content blocks, the agent loop and middleware. Deep Agents, in turn, builds on LangChain.

The vulnerabilities are presented as illustrating a general pattern rather than a defect peculiar to this library: any design in which model output is used to build a call to an external service inherits the same exposure, which the analysis traces to [[DefinedTerm/control-data-plane-confusion]]. Its recommendation to developers writing their own chains is to treat all model output as potentially malicious, parameterize templates and external calls, and apply least privilege across the entities contributing to a prompt.
