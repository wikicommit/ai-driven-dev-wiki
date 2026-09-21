---
title: "AI Teammate Lifecycle Engineering（ATLE）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/ai-teammate-lifecycle-engineering.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）において提案されているエンジニアリング活動で、エージェントに永続的な記憶と長期的なコンテキストを与え、状態を持たない使い捨ての請負人から、タスクをまたいで学び成長し続けるチームメイトへと進化させることを目的とする。"
---

AI Teammate Lifecycle Engineering（ATLE）とは、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] において [[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として提案された、構造化されたエンジニアリング活動のひとつである。同論文では「SE for Agents」という枠組みのもとで [[DefinedTerm/ai-teammate-infrastructure-engineering]]（ATIE）と対をなすものとして位置づけられている。その目的として掲げられているのは、エージェントが記憶を保持し時間をかけて学習できるようにすること — すなわち、あらゆるタスクをゼロから始める「使い捨ての請負人」から、組織的な知識を保持し続ける「生涯にわたるパートナー」へとエージェントを移行させることである。

## 使われ方

論文は ATLE を永続的な記憶に根ざしたものとして説明する。プロジェクトの履歴や意思決定ログの長期記憶を埋め込まれたエージェントは、コーチが同じ指示を何度も与えなくてもタスクをまたいだ連続性を保つ。その初期の例として挙げられているのが [[SoftwareApplication/devin]] が用いる DeepWiki であり、エージェントが自らのドキュメントと意思決定ログを構築し、タスクをまたいでそれを参照する事例とされている。ATLE はさらに、能動的な保守もその範囲に含む。永続的な記憶とコードベースへのアクセスを持つエージェントが、計算資源の空き時間にスケジュールされて技術的負債を走査し、ドキュメントの欠落を特定し、リファクタリングを提案する — そうした提案は新たな [[DefinedTerm/briefingscript]] として登録され、人間によるレビューを経る標準ワークフローに乗る。論文の ATLE に関する研究ロードマップが求めているのは、プロジェクト履歴・意思決定ログ・アーキテクチャ上の論拠を保持する仕組み（継続学習の手法と、グラフ・ベクトルストア・意思決定記録といった外部記憶構造の双方を含み、コンテキストウィンドウの溢れを避けるための SE 固有の圧縮を伴う）、チームをより優先度の高い開発から逸らすことなく能動的な保守作業をスケジュールし価値づけるための研究、そして逸話ではなく実証的・経済的なモデルによって、エージェント型 SE が長年の原則の背後にあるコストモデルをどう変えるかを示すこと（たとえばコードの重複は、エージェントにとっては一貫して更新しやすいものになる）である。

## 関連用語

[[DefinedTerm/ai-teammate-infrastructure-engineering]], [[DefinedTerm/agent-execution-environment]], [[DefinedTerm/structured-agentic-software-engineering]]
