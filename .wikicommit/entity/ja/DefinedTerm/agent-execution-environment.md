---
title: "Agent Execution Environment（AEE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-execution-environment.md"
source_commit: "f3cd768971749927e49083efe4fbd9f44cf27fb0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）において、エージェントのために提案されたワークベンチ。従来の IDE の人間中心のインターフェースではなく、高速な計算、大規模な並列性、構造化された機械可読のフィードバックといった、エージェント本来の強みに最適化されたデジタルワークベンチである。"
---

Agent Execution Environment（AEE）は、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] が [[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として提案する 2 つの専用ワークベンチの 1 つであり、人間のコーチ向けの [[DefinedTerm/agent-command-environment]]（ACE）と対をなす。論文は、人間の認知負荷を減らすよう最適化されたツールは、エージェントにとってはしばしば最適でないと論じる。エージェントは人間の認知的な限界に縛られておらず、むしろ計算効率に最適化された生の低オーバーヘッドなツールと、構造化された機械可読のフィードバックによって力を発揮するからである。その不一致の証拠として、今日の自律型コーディングエージェントの多くがいまだに grep のような基本的なユーティリティに頼っているという事実を挙げている。

## 用法

論文によれば、AEE には、膨大な状態空間を解析できるハイパーデバッガ、強力なセマンティック検索ユーティリティ、コードを単なるテキストではなく抽象的な記号構造として操作する構造エディタといった、エージェントネイティブなツールが必要である。また、エージェントの運用上の健全性を管理する監視インフラも備えていなければならない。すなわち、セキュリティ脆弱性を自律的に発見し、想定外に高い計算コストを生じさせているエージェントにフラグを立て、壊れた仮想環境を修復または置き換えることで、人間による戦略的な介入を要する問題だけが ACE に上がってくるようにする。ACE で定義された [[DefinedTerm/loopscript]] は、AEE の中でエージェントによって実行される。このエージェント中心の基盤を構築することは、Platform Engineering コミュニティの専門領域に属するとされている。

## 関連用語

[[DefinedTerm/agent-command-environment]]、[[DefinedTerm/structured-agentic-software-engineering]]
