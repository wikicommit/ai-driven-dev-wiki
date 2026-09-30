---
title: "ToolACE: Winning the Points of LLM Function Calling"
type: "schema:ScholarlyArticle"
lang: en
tags: [tool-use, function-calling, synthetic-data, llm-training]
sources:
  - type: url
    url: 'https://proceedings.iclr.cc/paper_files/paper/2025/file/663865ea167425c6c562cb0b6bcf76c7-Paper-Conference.pdf'
    hash: sha256:eda1e7bfde3691773f4fbfe174e85a48136c679d656a6734de89a1783df82bb1
review_status: pending
generated_at: "2026-09-30"
generated_by: "claude-opus-5-5"
generated_with: "0.8.0"

properties:
  description: "An ICLR 2025 conference paper presenting ToolACE, an automatic agentic pipeline for synthesizing accurate, complex and diverse function-calling training data, and showing that an 8B model fine-tuned on that data reaches results comparable to GPT-4 models on function-calling benchmarks."
  author: ["Weiwen Liu", "Xu Huang", "Xingshan Zeng", "Xinlong Hao", "Shuai Yu", "Dexun Li", "Shuai Wang", "Weinan Gan", "Zhengying Liu", "Yuanqing Yu", "Zezhong Wang", "Yuxian Wang", "Wu Ning", "Yutai Hou", "Bin Wang", "Chuhan Wu", "Xinzhi Wang", "Yong Liu", "Yasheng Wang", "Duyu Tang", "Dandan Tu", "Lifeng Shang", "Xin Jiang", "Ruiming Tang", "Defu Lian", "Qun Liu", "Enhong Chen"]
  keywords: ["[[DefinedTerm/function-calling]]", "tool learning", "synthetic data"]
---

This paper, published as a conference paper at ICLR 2025 by authors from Shanghai Jiao Tong University, Huawei Noah's Ark Lab, the University of Science and Technology of China, Huawei Technologies, Tsinghua University and the Chinese University of Hong Kong, addresses the training data behind [[DefinedTerm/function-calling]]. Its starting point is that collecting and annotating real function-calling data is hard, while synthetic data from existing pipelines often lacks coverage and accuracy, and that existing tool-augmented models mainly rely on public APIs and simple, single-turn calls.

It proposes ToolACE, an automated agentic pipeline with three modules. Tool Self-Evolution Synthesis (TSS) builds a hierarchical API context tree from API-related documents in pretraining data and uses a speciation–adaptation–evolution process to synthesize an API pool of 26,507 APIs. Self-Guided Dialog Generation (SDG) produces dialogs through role-play among simulated user, assistant and tool agents, while the model to be trained acts as a complexity evaluator so that generated data is neither too easy nor too hard for it. A Dual-Layer Verification (DLV) system combines a rule checker with model-based checks to keep the data accurate. The resulting data is released in part as [[Dataset/toolace]], and a model trained on it, ToolACE-8B, is evaluated on [[Dataset/berkeley-function-calling-leaderboard]] and API-Bank.

## Key Points

- The paper describes itself as, to the authors' knowledge, the first work to highlight the benefits of synthesizing diverse APIs to improve the generalization of function calls.
- It measures a data sample's complexity for a given model as that model's loss on the sample, and reports that loss generally rises with the number of candidate APIs, the number of APIs used and the dissimilarity between the query and the API descriptions — which it takes as validating loss as a complexity measure for function calling.
- The rule layer of verification checks API definition clarity, function-call executability, dialog correctness and data-sample consistency without executing calls; the model layer splits the check into hallucination detection, consistency validation and tool-response checking, each handled by a separate LLM-powered expert agent.
- ToolACE-8B is LLaMA-3.1-8B-Instruct fine-tuned with LoRA on the synthesized data. On the BFCL-v3 leaderboard as of 20 September 2024 it ranked third overall with 59.22, behind two GPT-4 models, and led the listed models on non-live executable accuracy; on API-Bank it outperformed all listed open-source models and was comparable to GPT-4-series models.
- Ablations report that the model checker adds to the rule checker's effect, that a medium-complexity subset trains slightly better than easy or hard subsets, and that more API diversity improves overall accuracy and especially irrelevance detection.
- Removing multi-type samples from the training mix dropped irrelevance detection to 6.99% on BFCL, and removing parallel-call samples sharply reduced the ability to invoke several tools at once.
- Using the model being trained as its own complexity evaluator gave better BFCL results than using a separate Qwen1.5-7B or Qwen1.5-14B evaluator in the authors' comparison.
- Fine-tuning on the data improved function calling across Qwen1.5 models from 0.5B to 7B and across three roughly 8B backbones, and the paper reports negligible degradation on some general-ability benchmarks relative to raw LLaMA-3.1-8B-Instruct, though ToolACE-8B still trails GPT-4 on reasoning and understanding.

## Notes

The authors list two limitations: the cost of computing data complexity grows with model size and sample count, and non-uniform sampling may bias training toward the model's comfort zone; and although the model is competitive at function calling, it lags GPT-4 in other capabilities, leaving open how to improve several capabilities at once. They suggest collaboration among multiple small, domain-specific agents as one direction. An appendix also reports that three-shot in-context learning on LLaMA-3.1-8B-Instruct performed far below fine-tuning on the same benchmark.
