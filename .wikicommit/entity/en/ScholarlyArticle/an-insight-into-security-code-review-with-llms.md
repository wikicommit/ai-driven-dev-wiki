---
title: "An Insight into Security Code Review with LLMs: Capabilities, Obstacles, and Influential Factors"
type: "schema:ScholarlyArticle"
lang: en
tags: [code-review, security, hallucination, prompting]
sources:
  - type: url
    url: 'https://arxiv.org/pdf/2401.16310'
    hash: sha256:68d2fba8f757c9789995cbb7728c6a9074f36cf7747bdaba59f8d6721cbfc647
review_status: pending
generated_at: "2026-09-25"
generated_by: "claude-opus-5-5"
generated_with: "0.7.0"

properties:
  description: "An empirical study of LLMs in security code review that evaluates seven LLMs under several prompts on 534 real code files with reviewer-identified security defects from OpenStack and Qt, finding that LLMs significantly outperform static analysis tools, with DeepSeek-R1 best and GPT-4 via ChatGPT second, while their responses still show frequent quality problems and hallucinations."
  author: ["Jiaxin Yu", "Peng Liang", "Yujia Fu", "Amjed Tahir", "Mojtaba Shahin", "Chong Wang", "Yangxiao Cai"]
  keywords: ["large language model", "code review", "security analysis"]
---

The paper studies how well large language models can support [[DefinedTerm/security-code-review]], asking for fine-grained output — the line number, type, description and suggested fix of each security defect — rather than the binary vulnerable/not-vulnerable judgment used in much earlier work. Its dataset is 534 code files (258 Python, 276 C/C++) from OpenStack Nova and Neutron and Qt Base and Creator, each carrying the file's source code, the commit message of its patchset, and the security defect a human reviewer identified in code review. Seven LLMs — GPT-4 via ChatGPT and via the API, GPT-4 Turbo, Gemini Pro, Llama 2 7B and 70B, and DeepSeek-R1 — were evaluated under five prompt templates (a basic prompt, added project information, a general CWE instruction, a specific list of first-level CWEs, and a two-step chain-of-thought prompt that first generates code context from the commit message), plus a guardrail variant for DeepSeek-R1 that keeps the commit message and step-by-step instruction without generated context, and compared with static analysis tools. Responses were manually rated as Instrumental, Helpful, Misleading or Uncertain, and each experiment was repeated three times.

For the two best models with their best prompts, the authors coded quality problems in the responses, mapped them onto a hallucination taxonomy, and fitted cumulative link regression models to test which of eleven factors — such as token count, defect position, file type, code complexity and annotations — influence detection.

## Key Points

- LLMs significantly outperformed the static analysis tools tested (SonarQube, CodeQL, Bandit and Semgrep for Python; CppCheck and Semgrep for C/C++); the reasoning-optimized model outperformed the general-purpose ones.
- DeepSeek-R1 performed best, followed by GPT-4 via ChatGPT; on the complete dataset DeepSeek-R1 did best with the guardrail prompt combining commit message and chain-of-thought guidance, while GPT-4 via ChatGPT did best with the specific CWE list.
- The authors still judge the capabilities of currently popular LLMs in security code review to be limited, with existing general-purpose LLMs falling significantly short of the effectiveness of manual security code review.
- Having the LLM generate missing code context from the commit message led to a performance decline for DeepSeek-R1, which the authors attribute to fabricated context that could contradict the actual code.
- GPT-4 via ChatGPT outperformed GPT-4 via the API and produced longer outputs (454 versus 94 tokens on average), which the authors suggest may partly reflect undisclosed platform-side optimizations.
- The two best-performing models had the least consistent responses across repeated runs, which the authors suggest may reflect reasoning along more varied paths.
- 20.19% of GPT-4 (ChatGPT) responses and 36.45% of DeepSeek-R1 responses contained at least one hallucination; GPT-4 (ChatGPT) was more prone to vague statements and poor instruction-following, while DeepSeek-R1 more often gave incorrect code details such as wrong line numbers (31.81% of its responses).
- Both models detected security defects better in files with fewer tokens and with security-related annotations; for DeepSeek-R1, higher cyclomatic complexity was associated with better detection for defect types other than memory-related ones.

## Notes

The authors suggest a multi-layered review strategy in which files are classified by difficulty, LLMs perform an initial review, and reviewers confirm or deepen the LLM's findings, and they call for investigating the right granularity for CWE lists in prompts. They list as threats possible overlap between the dataset and the models' training data, the use of a single file rather than a whole patchset as input, and a dataset of four open-source projects that may not represent industrial code. They also note that the statistical power for some factors, including DeepSeek-R1's token and complexity effects, was below 0.80.
