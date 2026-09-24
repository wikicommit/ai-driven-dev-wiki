---
title: "オーケストレーション税"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/orchestration-tax.md"
source_commit: "c6bf44a9d0262400c75a0abf7dee6a8fbb53ff80"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "Addy Osmani の基調講演「Own the Outer Loop」で示された捉え方で、並列に動く複数のコーディングエージェントを指揮しレビューすることの認知的なコスト — 悪い振る舞いから遠ざけるよう舵を取り、出力をトリアージし、走らせる前に重要な前提を検証すること — を指す。エージェントを増やすのが容易になったからといって、このコストが小さくなるわけではない。"
---

Addy Osmani は基調講演「Own the Outer Loop」において、オーケストレーション税（orchestration tax）を、並列に動く複数のコーディングエージェントを指揮しレビューすることの認知的なコストとして捉えている。エージェントを増やすことは容易になったが、人間自身の認知の帯域は同じようには並列化しない。エージェントを最悪の振る舞いから遠ざけるよう舵を取ること、生み出された作業をより分けて注意が必要なものを見つけること、最も重要なものへとエージェントを向けること、そして走らせる前に重要な制約と危険な前提を検証することは、いずれも自動化によって取り除くことのできない作業だと説明されている。

## 用法

出典によれば、この税はブラウンフィールドのシステムではより重くなる。監査が必要な振る舞いはコードの中にあるのではなく、出典自身の言葉で言えば「傷跡（the scars）」の中にあるからである。4 つの緩和策が挙げられている。アーキテクチャ上の判断に注意を優先的に振り向けること、ワークツリー、スコープ、証拠を用いて当初の計画とそこから生まれる作業との結合を弱めること、実行に移せないステップの解決に費やす労力に時間の上限を設けること、そしてソフトウェアへの変更を厳格にオプトインにすることである。これは、認知的降伏および認知的負債と並ぶ、エージェントへの委任の 3 つの隠れたコストの 1 つとして示されている。

## 関連用語

[[DefinedTerm/outer-loop]]、[[DefinedTerm/cognitive-surrender]]、[[DefinedTerm/cognitive-debt]]
