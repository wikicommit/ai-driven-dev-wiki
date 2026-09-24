---
title: "MentorScript"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/mentorscript.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-24"
translated_by: "claude-opus-5-5"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている、構造化されバージョン管理された規則集。プロジェクトの規範とベストプラクティスの指針を「コードとしてのメンタリング（mentorship-as-code）」としてエージェント向けに成文化し、暗黙的でその場限りのコードレビューのコメントに取って代わる。"
---

MentorScript とは、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）が、エージェント向けにチームの規範とベストプラクティスを成文化するために提案する成果物であり、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] において [[DefinedTerm/ai-teammate-mentorship-engineering]]（ATME）の産物として導入された。同論文はこれを、メンタリングを暗黙的でその場限りの活動 — コードレビューでのコメント — から、明示的で発展し続ける成文化された営みへと変えるものと位置づけ、「コードとしてのメンタリング（mentorship-as-code）」と呼んでいる。

## 用法

MentorScript には、粒度の細かいチェック（たとえば「新しい関数にはすべて決定的なテストがなければならない」）から高水準の原則に至るまでの規則を収めることができる。同論文は、そうした規則を原子的かつ決定的に保つために、規則そのものも独自の品質ゲート — lint、単体テスト、衝突検出 — の対象とすべきだと述べている。指針は、明示的で永続的なもの（人間のコーチが、エージェントが同じ誤りを繰り返さないよう捉えておく、直接的で一般化可能な修正）である場合もあれば、推論されたもの（エージェントが特定の文脈での修正から新たな一般規則を提案し、コーチがそれを承認するもの）である場合もある。同論文は、エージェントの振る舞いが期待から外れたときに迅速な根本原因分析を可能にするため、エージェントが取るあらゆる行動は、プロンプト解釈と推論の可観測性の技法を用いて、考慮された MentorScript の規則まで遡って追跡できるべきだと述べている。また、CLAUDE.md、`.clinerules`、AGENT.md といったプロジェクトレベルの設定ファイル（[[DefinedTerm/agents-md]] を参照）を、MentorScript に類する成果物の初期の草の根的な例として挙げ、そうしたファイルに何をどの程度の詳しさで記すべきかについて、コミュニティにはまだ合意がないと指摘している。

## 関連用語

[[DefinedTerm/ai-teammate-mentorship-engineering]]、[[DefinedTerm/agents-md]]、[[DefinedTerm/briefingscript]]
