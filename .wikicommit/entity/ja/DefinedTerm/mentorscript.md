---
title: "MentorScript"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/mentorscript.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている、構造化されバージョン管理されたルールブック。プロジェクトの規範やベストプラクティスに関するエージェント向けの指針を「コードとしてのメンタリング（mentorship-as-code）」として成文化し、暗黙的で一過性のコードレビューコメントに取って代わるもの。"
---

MentorScript とは、エージェント向けにチームの規範とベストプラクティスを成文化するために [[DefinedTerm/structured-agentic-software-engineering]]（SASE）が提案しているアーティファクトであり、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] において [[DefinedTerm/ai-teammate-mentorship-engineering]]（ATME）の成果物として導入されている。論文はこれを、メンタリングを暗黙的で一過性の活動（コードレビューでのコメント）から、明示的で進化し続ける成文化された規律へと転換するものと位置づけ、それを「コードとしてのメンタリング（mentorship-as-code）」と呼んでいる。

## 用法

MentorScript には、細かなチェック（たとえば「新しい関数にはすべて決定論的なテストがなければならない」）から高レベルの原則に至るまで、さまざまなルールを収めることができる。論文は、こうしたルール自体にも独自の品質ゲート（リンティング、単体テスト、競合検出）を適用し、ルールを原子的かつ決定論的に保つべきだと述べている。指針は、明示的で永続的なもの（エージェントが同じ誤りを繰り返さないよう、人間のコーチが記録する直接的で一般化可能な修正）である場合もあれば、推論されたもの（エージェントが特定の文脈での修正から新たな一般ルールを提案し、コーチがそれを承認するもの）である場合もある。論文は、エージェントの振る舞いが期待から外れたときに迅速な根本原因分析を可能にするため、プロンプト解釈や推論の可観測性の技術を用いて、エージェントが取るあらゆる行動を、考慮された MentorScript のルールまでさかのぼって追跡できるようにすべきだとしている。また、CLAUDE.md、`.clinerules`、AGENT.md といったプロジェクトレベルの設定ファイル（[[DefinedTerm/agents-md]] を参照）を、MentorScript 的なアーティファクトの初期の草の根的な例として挙げ、こうしたファイルに何をどの程度の詳しさで記述すべきかについて、コミュニティにはまだ合意がないと指摘している。

## 関連用語

[[DefinedTerm/ai-teammate-mentorship-engineering]], [[DefinedTerm/agents-md]], [[DefinedTerm/briefingscript]]
