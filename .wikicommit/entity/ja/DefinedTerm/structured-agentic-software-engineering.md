---
title: "Structured Agentic Software Engineering（SASE）"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/structured-agentic-software-engineering.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "エージェント型ソフトウェアエンジニアリング（SE3.0）の時代に向けて提案されたエンジニアリング分野。ソフトウェアエンジニアリングの 4 つの柱 — アクター、プロセス、ツール、成果物 — を、人間のための SE とエージェントのための SE という二元性を軸に再構想し、両者を専用のワークベンチとバージョン管理された成果物で結びつける。"
---

Structured Agentic Software Engineering（SASE）は、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で提案されたビジョンであり、エージェント型ソフトウェアエンジニアリング（SE3.0）を構造化され、予測可能で、信頼できるものにすることを目指している。これは二元性に立脚している。この分野は、人間のための SE（SE4H）と、エージェントのための SE（SE4A）の双方に同時に奉仕しなければならない。SE4H は人間の役割を、「エージェントコーチ（Agent Coach）」として高レベルの意図、戦略、メンタリングを担うものへと再定義し、SE4A は複数のエージェントが効果的に動作できる、構造化された予測可能な環境を確立する。この二元性をまたいで、SASE はソフトウェアエンジニアリングの伝統的な 4 つの柱を再構想する。アクターは人間の開発者から、人間の「エージェントコーチ」と専門化されたエージェントからなるハイブリッドなチームへと拡張される。プロセスはアドホックなプロンプティングを、構造化され反復可能なエンジニアリング活動に置き換える。成果物は一時的なプロンプトではなく、永続的で機械可読な、バージョン管理されたドキュメントとなる。そしてツールは、人間中心の単一の IDE の代わりに、目的特化の 2 つのワークベンチに分かれる。

## 用法

SASE は 2 つの専用ワークベンチ — 人間のコーチのための [[DefinedTerm/agent-command-environment]]（ACE）と、エージェントのための [[DefinedTerm/agent-execution-environment]]（AEE）— によって運用され、両者はバージョン管理された成果物による構造化された対話で結ばれる。人間は [[DefinedTerm/briefingscript]]、[[DefinedTerm/loopscript]]、[[DefinedTerm/mentorscript]] によって作業を開始し、エージェントは [[DefinedTerm/consultation-request-pack]] または [[DefinedTerm/merge-readiness-pack]] で応答し、人間はそれに対して [[DefinedTerm/version-controlled-resolution]] で対処する。5 つの名前付きエンジニアリング活動がこの対話を運用する。[[DefinedTerm/briefing-engineering]]、[[DefinedTerm/agentic-loop-engineering]]、[[DefinedTerm/ai-teammate-mentorship-engineering]]、[[DefinedTerm/agentic-guidance-engineering]]、そして共同の [[DefinedTerm/ai-teammate-lifecycle-engineering]]/[[DefinedTerm/ai-teammate-infrastructure-engineering]] の分野である。論文は、多数の人間と多数のエージェントによるこのチームレベルの N 対 N の協働を、論文が「エージェント型コーディング」と呼ぶもの — 一人の開発者と 1 つの AI アシスタントとの間の、現在の主に 1 対 1 のやり取り — と区別している。

## 適用される場面

論文は SASE を、実装されたシステムではなく意図的にビジョナリーなものとして提示している。決定的な解決策ではなく、コミュニティの対話を促すための概念的な足場として提示されており、著者らはコミュニティに対し、それが提案するエンジニアリング活動に異議を唱え、洗練し、拡張するよう呼びかけている。論文は、SASE が、計算資源によってスケールする汎用的な手法が手作りの構造を上回るという Richard Sutton の「Bitter Lesson（苦い教訓）」に反するものではないと論じている。その教訓が最も強く当てはまるのは訓練データが豊富な場面（例えば一般的な Web アプリケーションの構築）であり、全体を貫く構造を与えるためにまだ人間が必要とされる新規のタスクやニッチな領域では弱まる、というのがその理由である。論文自身の具体例 — ある開発者が、エージェントチームを起動して 28 個の候補プルリクエストを並列に生成させることで 7 つのプルリクエストを解決する — は、SASE が対処しようとするプロセスと成果物のギャップを例示するものであって、SASE 自体の実運用の事例ではない。

## 関連用語

[[DefinedTerm/agent-command-environment]], [[DefinedTerm/agent-execution-environment]], [[DefinedTerm/se-autonomy-levels]]
