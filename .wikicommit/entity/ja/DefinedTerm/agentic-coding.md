---
title: "エージェンティックコーディング"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェンティックコーディング, AI支援プログラミング, 用語]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agentic-coding.md"
source_commit: "1804b4f09d8e8e88510a78cca5839eb041febbe0"
translated_at: "2026-08-20"
translated_by: "claude-opus-5[1m]"

properties:
  description: "ソフトウェア開発に AI エージェントを用いること。プロンプトにテキストで応答するだけでなく、開発環境と自律的にやり取りし、コマンドやテストを実行し、目標に向かってコードを反復的に改善していくツールを指す。"
  termCode: ""
  inDefinedTermSet: ""
---

エージェンティックコーディングとは、ソフトウェア開発に AI エージェントを用いることであり、プロンプトに対して生成されたテキストを返すだけの AI とは区別される。これは [[DefinedTerm/ai-assisted-software-development]] の部分集合であり、ツールが開発環境の中で行動を取る——ファイルを読み、コマンドやテストを実行し、その結果に反応し、反復する——点に特徴がある。そもそも無人あるいは半監視のセッションが成り立つのは、このためである。

## 用法

実務上、この語は特定のツールではなく働き方のモードを指す。[[BlogPosting/the-role-of-developer-skills-in-agentic-coding]] における Böckeler の記述は、2025年初頭時点で彼女が使った IDE 統合型のエージェンティックモードに何ができたのかを描いている。テストやその他の開発タスクを実行して発生したエラーを即座に修正しようとすること、リント・コンパイルエラーを自動的に検知して修正を試みること、ウェブでの調査を行うこと、そして場合によってはブラウザプレビューとの統合によってコンソールのエラーを読んだり DOM 要素を調べたりすることである。彼女は自分が実際に取った働き方を「監督されたエージェント」モードと特徴づける。絶えず介入し、修正し、方向づけを行うモードである——そして、それが要求する開発者スキルこそ保全し訓練する価値のあるものだと論じる。その監督が欠けたときに何がまずくなるかについての彼女の分類は [[DefinedTerm/impact-radius]] で扱われている。

Anthropic の [[Report/2026-agentic-coding-trends-report]] は、同じ実践を別の視点から、すなわち先の一年を予測するベンダーの立場から描いている。その中心的な枠づけは、エンジニアの役割が実装者からオーケストレーターへ移るというものである。貢献の価値はシステムアーキテクチャの設計、エージェントの調整、品質の評価、戦略的な問題分解へと移り、人間の主たる役割は、コードを書くエージェントをオーケストレーションし、その出力を評価し、システムが正しい問題を解いていることを保証することになる。レポートはまた、コラボレーションのパラドックスと呼ぶ緊張も報告している——開発者は業務のおよそ 60% で AI を使いながら、「完全に委譲できる」タスクは 0〜20% にすぎないと答えている——。レポートはこれを、エージェンティックコーディングは引き継ぎではなく本質的に協働的なものだと論じることで解消する。エンジニアは検証が容易な作業、定義が明確な作業、反復的な作業を委譲し、設計に依存する判断は自分の手元に残す、というわけである。

この2つの記述は、実践の形については一致しつつ、調子において異なっている。一方は絶えざる人間の舵取りを、設計によって回避すべき制約として捉え、もう一方はそれを意図された運用モデルとして捉えている。

## 関連用語

エージェンティックコーディングは [[DefinedTerm/ai-assisted-software-development]] の下に位置し、[[DefinedTerm/coding-agent]] で扱われるツールによって実行される。これを構造化する名前付きの方法論には [[DefinedTerm/agentic-engineering]]、[[DefinedTerm/vibe-engineering]]、[[DefinedTerm/spec-driven-development]]、[[DefinedTerm/subagent-driven-development]]、[[DefinedTerm/ralph]] がある。その中心的なエンジニアリング上の制約は [[DefinedTerm/context-engineering]] で、複数のエージェントを同時に調整することは [[DefinedTerm/multi-agent-orchestration]] で扱われている。
