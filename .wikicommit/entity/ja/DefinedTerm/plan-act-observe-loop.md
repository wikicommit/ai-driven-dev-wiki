---
title: "Plan-Act-Observe ループ"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/plan-act-observe-loop.md"
source_commit: "c6bf44a9d0262400c75a0abf7dee6a8fbb53ff80"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "コーディングエージェントがたどる中核的な反復サイクル。アプローチを計画（plan）し、コードを書いたり編集したりして行動（act）し、結果を観察（observe）し、観察した内容にもとづいてこれを繰り返す。"
---

Plan-Act-Observe ループは、コーディングエージェントが作業中にたどる中核的なサイクルである。エージェントはアプローチを計画し、それにもとづいて行動し、結果を観察し、その観察を使って次のステップを計画する。計画のフェーズでは、エージェントはタスクを読み、関連するコードを調べ、アプローチを決める。行動のフェーズでは、コードを書き、ファイルを編集し、コマンドを実行する。観察のフェーズでは、コンパイラの出力、テスト結果、エラーメッセージを確認する。このサイクルは、エージェントがタスクを完了するか、上限（トークン予算、時間制限、最大反復回数）に達するか、行き詰まって助けを求めるまで繰り返される。

## 用法

エージェントは行動の前に計画するので、コンテキストを前もって与えておくと計画のフェーズを改善できる。また、エージェントは結果を観察するので、より明確なフィードバック——テストの出力、エラーメッセージ、型チェック——を与えると観察のフェーズが改善される。各フェーズの質は、エージェントが正しい解にどれだけ早く収束するかに影響する。より良い計画はより一貫性のある最初の試みを生み、より良い観察（問題が単に抑え込まれたのではなく本当に修正されたときにそれを見分けること）は収束を速める。既知の失敗モードとして、エージェントが 2 つの修正のあいだを行き来して抜け出せなくなり、それぞれが他方の直したものを壊してしまうというものがあり、反復回数に対するガードレールはこれを抑えるためのものである。

## 関連用語

[[DefinedTerm/ai-coding-agent]], [[DefinedTerm/tool-use]], [[DefinedTerm/chain-of-thought]], [[DefinedTerm/guardrails]], [[BlogPosting/self-improving-agents]]
