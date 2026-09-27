---
title: "rLLM"
type: "schema:SoftwareApplication"
lang: ja
tags: [強化学習, オープンソース, トレーニング]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/rllm.md"
source_commit: "4438c05fa3a3f4ca959d0a98e469711dd675b69b"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "強化学習によって言語エージェントを事後学習するための、Agentica のオープンソースフレームワーク。DeepSWE-Preview コーディングエージェントの学習に使われた。"
  applicationCategory: "言語エージェントを事後学習するためのフレームワーク"
  author: "Agentica"
---

rLLM は、言語エージェントを事後学習するための Agentica のオープンソースフレームワークである。[[BlogPosting/deepswe-training-a-fully-open-sourced-state-of-the-art-coding-agent-by-scaling-rl]] において、rLLM は DeepSWE-Preview コーディングエージェントの学習に使われたシステムであり、同チームの以前のリリースである DeepCoder-14B-Preview と DeepScaleR-1.5B-Preview も同じくこれで学習された。この記事は DeepSWE-Preview を rLLM によって実現されたものと説明し、チームのミッションを LLM のための強化学習（RL）の民主化だと述べている。

記事の貢献者に関する記載では、rLLM に関する作業が DeepSWE プロジェクトの一部として説明されている。すなわち、rLLM のためのエージェントと環境の抽象化の実装、その性能の最適化、そして DeepSWE の学習に使われた最初の rLLM システムの設計と実装である。
