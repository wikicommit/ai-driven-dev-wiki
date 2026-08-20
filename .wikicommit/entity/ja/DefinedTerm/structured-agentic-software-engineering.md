---
title: "Structured Agentic Software Engineering"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェンティックコーディング, ソフトウェア開発プロセス, 人間とAIの協働, 用語]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/structured-agentic-software-engineering.md"
source_commit: "1804b4f09d8e8e88510a78cca5839eb041febbe0"
translated_at: "2026-08-20"
translated_by: "claude-opus-5[1m]"

properties:
  description: "Hassan らがエージェンティックソフトウェアエンジニアリングの時代のために提案した概念フレームワーク。SE for Humans と SE for Agents の二重性、目的別に作られた2つのワークベンチ、そして人間とエージェントのやり取りを担うバージョン管理された成果物の集合を軸に組織されている。"
  termCode: "SASE"
---

Structured Agentic Software Engineering（SASE）は、Ahmed E. Hassan らが [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] において、[[DefinedTerm/agentic-software-engineering]] を構造化され、予測可能で、信頼に足るものにするために提案した概念フレームワークである。その中核となる主張は *構造化された二重性* である。この分野は共生する2つのモダリティを同時に支えなければならない。SE for Humans（SE4H）は、人間の役割を高水準の意図、戦略、そして「エージェントコーチ」としてのメンターシップを軸に再定義する。SE for Agents（SE4A）は、複数のエージェントが効果的に動作できる構造化され予測可能な環境を確立する。著者らはこれを、検証された方法論ではなく、コミュニティの対話を促すことを意図した先見的な概念の足場として提示している。

## 用法

SASE は、この二重性がソフトウェアエンジニアリングの4つの基礎的な柱の再考を要求すると提案する。それぞれが2つのモダリティにおいて異なる形で現れるからである。

| 柱 | SASE が提案する転換 |
| --- | --- |
| アクター | 人間の開発者から、人間の「エージェントコーチ」と専門化されたソフトウェアエージェントからなるハイブリッドなチームへ |
| プロセス | 場当たり的なプロンプトから、人間とエージェントの協働を統べる構造化され反復可能なエンジニアリングの活動へ |
| 成果物 | 束の間の非公式なプロンプトから、契約であり組織の記憶でもある永続的で機械可読な成果物へ |
| ツール | 人間中心のオールインワンの IDE から、人間用とエージェント用に専門化されたワークベンチへ |

ツールの柱について、SASE は IDE を2つの環境で置き換えることを提案する。人間のコーチのための [[DefinedTerm/agent-command-environment]] と、エージェントのための [[DefinedTerm/agent-execution-environment]] である。両者の間のやり取りは、非公式なチャットの独白ではなく、明示的でバージョン管理された成果物によって担われる——人間は [[DefinedTerm/briefing-script]]、LoopScript、MentorScript を執筆する。エージェントは [[DefinedTerm/consultation-request-pack]] と [[DefinedTerm/merge-readiness-pack]] を生み出す。そして人間は、対象の成果物に明示的にリンクされた Version Controlled Resolution で応答する。

このフレームワークは、単一のプロセスではなく名前の付いた一連のエンジニアリング活動を通じて運用される。Briefing Engineering（BriefingEng）、Agentic Loop Engineering（ALE）、AI Teammate Mentorship Engineering（ATME）、Agentic Guidance Engineering（AGE）、そして AI Teammate Lifecycle and Infrastructure Engineering（ATLE と ATIE）である。論文はこの一覧を決定版でも網羅的でもない初期の足場として提示し、コミュニティに異議を唱え拡張することを呼びかけている。

繰り返し強調されるのは、SASE が単独作業の支援ではなくチーム規模の作業を対象としている点である。著者らは *エージェンティックコーディング*——開発者と AI アシスタントの1対1のやり取りであり、単独作業の拡張として枠づけられる——と、多数の人間と多数のエージェントの間の N対N の協働を支えなければならない *エージェンティックソフトウェアエンジニアリング* を区別する。SASE はまた、ソフトウェアエンジニアリングが硬直的で普遍的なプロセスが無力な「厄介な問題」であることを認め、それゆえに、特定のチームの文脈へ素早くオンボードされた AI チームメイトのほうが、優秀だが脆い専門特化のエージェントよりも価値があると論じる。

## 関連用語

SASE は [[DefinedTerm/agentic-software-engineering]] に対する競合する複数の枠づけの一つである。著者らはこれを、Plan-Do-Assess-Review 流のループ、Product Requirement Prompt 流のブリーフ、そして BMAD のようなマルチエージェントのフレームワークの上に築かれたものと位置づけつつ、コードとしてのメンターシップ、2つのワークベンチ、目標成果物としてのマージ準備状態、そして一級の成果物としてのコンサルタビリティによって自らを差別化している。
