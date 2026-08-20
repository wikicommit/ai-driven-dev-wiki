---
title: "Consultation Request Pack"
type: "schema:DefinedTerm"
lang: ja
tags: [エージェンティックコーディング, 人間とAIの協働, 用語]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/consultation-request-pack.md"
source_commit: "1804b4f09d8e8e88510a78cca5839eb041febbe0"
translated_at: "2026-08-20"
translated_by: "claude-opus-5[1m]"

properties:
  description: "Structured Agentic Software Engineering フレームワークにおいて、エージェントがタスクの途中で人間の専門知識を求めるために生成する構造化された成果物。具体的な不確実性や意思決定点を、選択肢、トレードオフ、推奨とともに文書化する。"
  termCode: "CRP"
---

Consultation Request Pack（CRP）は、[[DefinedTerm/structured-agentic-software-engineering]] においてエージェント発の人間へのコンサルテーションのために提案された成果物である。エージェントが先に進むために人間の入力を必要とするときに生成され、具体的な不確実性や意思決定点を、チャットログ上の開かれた問いとしてではなく構造化された形で文書化する。[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] はこれを、人間とエージェントのパートナーシップを双方向にする仕組みとして提示している。エージェントは指示を受けるだけでなく、人間を呼び出すこともできるのである。

## 用法

CRP は有効な [[DefinedTerm/briefing-script]] によって文脈づけられ、LoopScript や MentorScript のルールによってトリガーされうる。論文の具体例では、意思決定点を軸に、課題の要約と詳細、それぞれに利点・欠点・見積もり工数を伴うラベル付きの選択肢の集合、理由を添えた明示的なエージェントの推奨、求められている具体的な意思決定、そして誰が決めるべきかの役割を指名するエスカレーション先という構成になっている。

ルーティングは [[DefinedTerm/agent-command-environment]] が担い、要求を提示し記録する。論文はこれを、説明責任に必要なコンテキストを保持したまま、ACE が人間を呼び出し可能な専門知識のエンドポイントとして扱うことだと説明している。挙げられている例は、エージェントがデータベーススキーマの問題を指名されたデータベースアーキテクトにルーティングし、そのアーキテクトが ACE を通じてフィードバックを返すというものである——そして著者らは、より進んだ状況ではその「アーキテクト」の役割自体が別の専門化されたエージェントによって埋められるかもしれないと注記している。

人間の応答は非公式な返信ではない。このフレームワークにおいて、CRP をレビューし回答することは Agentic Guidance Engineering（AGE）と呼ばれる活動に属し、対象の成果物に明示的にリンクされた Version-Controlled Resolution（VCR）を生む。これによってトレーサビリティが保たれ、下流での監査と学習が可能になる。ACE は CRP をトリアージするための受信箱のようなインタフェースを提供するものと規定されている。

論文は、CRP こそが人間を出力の受動的な承認者から、その専門性が最も価値を生む地点にぴたりと介入する能動的でオンデマンドのコンサルタントへと引き上げるものであり、この種の明示的で持続的な成果物がなければ、複数の主体が関わるワークフローは束の間の、追跡不能で、結局のところ管理不能なものになると論じる。著者らは「一級の成果物としてのコンサルタビリティ」を、自らのフレームワークを隣接する取り組みから区別する点の一つとして挙げ、CRP が追跡可能な役割横断の引き継ぎを可能にし、単独のエージェンティックコーディングからチームベースのエージェンティックソフトウェアエンジニアリングへとパラダイムを移すものだと説明している。

## 関連用語

CRP はこのフレームワークにおけるエージェント生成の2つの成果物の一つであり、もう一方は、エージェントが行き詰まったときではなく完了したときに提出される [[DefinedTerm/merge-readiness-pack]] である。エージェントは [[DefinedTerm/agent-execution-environment]] の内側から CRP を上げ、人間は [[DefinedTerm/agent-command-environment]] でそれをトリアージする。
