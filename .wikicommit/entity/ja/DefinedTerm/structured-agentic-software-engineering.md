---
title: "Structured Agentic Software Engineering（SASE）"
type: "schema:DefinedTerm"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/structured-agentic-software-engineering.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "エージェント型ソフトウェアエンジニアリング（SE3.0）の時代に向けて提案されたエンジニアリング分野。ソフトウェアエンジニアリングの 4 つの柱——アクター、プロセス、ツール、成果物——を、人間のための SE とエージェントのための SE という二元性を軸に捉え直し、両者を専用のワークベンチとバージョン管理された成果物によって結びつける。"
---

Structured Agentic Software Engineering（SASE）は、エージェント型ソフトウェアエンジニアリング（SE3.0）を構造化され、予測可能で、信頼できるものにするために [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で提案されたビジョンである。その土台には二元性がある。この分野は、人間の役割を高レベルの意図・戦略・メンタリングを担う「エージェントコーチ（Agent Coach）」へと再定義する人間のための SE（SE4H）と、複数のエージェントが効果的に動作できる構造化された予測可能な環境を確立するエージェントのための SE（SE4A）の両方に、同時に応えなければならない。この二元性をまたいで、SASE はソフトウェアエンジニアリングの伝統的な 4 つの柱を捉え直す。アクターは人間の開発者から、人間の「エージェントコーチ」と専門化したエージェントからなるハイブリッドなチームへと拡張される。プロセスは場当たり的なプロンプティングに代わり、構造化された反復可能なエンジニアリング活動となる。成果物は一時的なプロンプトではなく、永続的で機械可読な、バージョン管理されたドキュメントとなる。そしてツールは、人間中心の単一の IDE ではなく、目的に特化した 2 つのワークベンチに分かれる。

## 用法

SASE は 2 つの専用ワークベンチ——人間のコーチのための [[DefinedTerm/agent-command-environment]]（ACE）と、エージェントのための [[DefinedTerm/agent-execution-environment]]（AEE）——によって運用され、両者はバージョン管理された成果物による構造化された対話でつながっている。人間は [[DefinedTerm/briefingscript]]、[[DefinedTerm/loopscript]]、[[DefinedTerm/mentorscript]] によって作業を開始し、エージェントは [[DefinedTerm/consultation-request-pack]] または [[DefinedTerm/merge-readiness-pack]] で応答し、人間はそれに対して [[DefinedTerm/version-controlled-resolution]] で対処する。この対話を運用するのが、名前の付いた 5 つのエンジニアリング活動である。すなわち [[DefinedTerm/briefing-engineering]]、[[DefinedTerm/agentic-loop-engineering]]、[[DefinedTerm/ai-teammate-mentorship-engineering]]、[[DefinedTerm/agentic-guidance-engineering]]、そして [[DefinedTerm/ai-teammate-lifecycle-engineering]]/[[DefinedTerm/ai-teammate-infrastructure-engineering]] を合わせた分野である。論文は、多数の人間と多数のエージェントによるこのチームレベルの N 対 N の協働を、同論文が「エージェント型コーディング」と呼ぶもの——1 人の開発者と 1 つの AI アシスタントとの間の、現状ではおおむね 1 対 1 のやり取り——と区別している。

## 適用される場面

論文は SASE を、実装されたシステムではなく意図的にビジョンとして提示している。決定的な解決策ではなく、コミュニティでの対話を促すための概念的な足場として示されており、著者らはコミュニティに対し、提案したエンジニアリング活動に異を唱え、磨き上げ、拡張するよう呼びかけている。論文は、SASE が、計算量でスケールする汎用的な手法は作り込まれた構造に勝るという Richard Sutton の「苦い教訓（Bitter Lesson）」に反するものではないと論じる。この教訓が最も強く効くのは訓練データが豊富な場面（例：一般的な Web アプリケーションの構築）であり、全体の構造を与えるために依然として人間が必要とされる新規のタスクやニッチな領域では弱まるからである。論文自身の具体例——開発者が 7 件のプルリクエストを解決するために、エージェントのチームを起動して 28 件の候補プルリクエストを並列に生成させる——は、SASE そのものの運用事例ではなく、SASE が対処しようとするプロセスと成果物のギャップを例示するものである。

## 関連用語

[[DefinedTerm/agent-command-environment]], [[DefinedTerm/agent-execution-environment]], [[DefinedTerm/se-autonomy-levels]]
