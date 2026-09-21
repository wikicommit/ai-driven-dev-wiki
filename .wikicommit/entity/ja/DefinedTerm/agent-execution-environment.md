---
title: "Agent Execution Environment（AEE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/agent-execution-environment.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）におけるエージェントのために提案されたワークベンチ。従来の IDE がもつ人間中心のインターフェースではなく、高速な計算、大規模な並列性、構造化された機械可読フィードバックといったエージェント本来の強みに最適化されたデジタルワークベンチ。"
---

Agent Execution Environment（AEE）は、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] が
[[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として提案する、目的別に作られた 2 つの
ワークベンチの一方であり、もう一方は人間のコーチのための [[DefinedTerm/agent-command-environment]]（ACE）である。
論文は、人間の認知負荷を減らすよう最適化されたツールはエージェントにとってはしばしば最適でないと論じる。エージェント
は人間の認知的限界に縛られておらず、むしろ計算効率と構造化された機械可読フィードバックに最適化された、生の
オーバーヘッドの小さいツールでこそ力を発揮するからである。その証拠として、今日の自律的なコーディングエージェントの
多くがいまだに grep のような基本的なユーティリティに頼っているという事実を挙げている。

## 用法

論文は AEE について、膨大な状態空間を解析できるハイパーデバッガ、強力なセマンティック検索ユーティリティ、そしてコード
を単なるテキストではなく抽象的な記号構造として操作する構造エディタといった、エージェントネイティブなツールが必要だと
説明している。さらに、エージェントの運用上の健全性を管理するための監視インフラも含まれねばならない。セキュリティ
脆弱性を自律的に見つけ出し、予期せず高い計算コストを発生させているエージェントにフラグを立て、壊れた仮想環境を修復
または交換することで、戦略的な人間の介入を要する問題だけが ACE に上がってくるようにするのである。ACE で定義された
[[DefinedTerm/loopscript]] は AEE の内部でエージェントによって実行され、このエージェント中心の基盤を築くことは
プラットフォームエンジニアリングのコミュニティの専門領域に属すると説明されている。

## 関連用語

[[DefinedTerm/agent-command-environment]], [[DefinedTerm/structured-agentic-software-engineering]]
