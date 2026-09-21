---
title: "AI Teammate Mentorship Engineering（ATME）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/ai-teammate-mentorship-engineering.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-21"
translated_by: "claude-opus-5[1m]"
translated_with: "0.7.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）において提案されているエンジニアリング活動で、プロジェクトの規範とベストプラクティスを、バージョン管理された MentorScript を介した「メンターシップ・アズ・コード」としてエージェント向けに成文化し、指導が暗黙的で儚いものではなく、永続的かつ監査可能なものとなるようにする。"
---

AI Teammate Mentorship Engineering（ATME）とは、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] において [[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として提案された、構造化されたエンジニアリング活動のひとつである。その目的として掲げられているのは、エージェントが生成したコードが単に機能するだけでなく、保守可能でありチームの文化に沿ったものであることを保証することであり、そのためにエージェントへの指導をファーストクラスのコードとして扱う — 論文がいう「メンターシップ・アズ・コード」である。

## 使われ方

論文は ATME のもとでの指導を人間のコーチに割り当て、それをエージェントが永続的に消費するものとしている。ルールは [[DefinedTerm/agent-command-environment]]（ACE）で書かれ、[[DefinedTerm/agent-execution-environment]]（AEE）におけるエージェントの振る舞いに直接影響を与える。その成果物が [[DefinedTerm/mentorscript]] である。この活動に関する論文の研究ロードマップが求めているのは、細やかな指導を表現できるだけの表現力を持ちながら、チームが通常のエンジニアリング成果物としてレビューできるだけの単純さを備えた抽象化、メンターシップのルールそのものに対する品質保証 — リント、テスト、競合検出、リグレッションチェック、そして新しいルールが他所で意図しない副作用を生むことなくエージェントの振る舞いを改善しているかを検証する方法の研究 — 、そしてエージェントが人間からの繰り返しのフィードバックからルール候補を学習し説明する仕組みであり、しかもそれらのルールをレビュー可能かつ監査可能に保ち、エージェントの判断をそれが参照した具体的なルールに結びつけられるようにすることである。

## 関連用語

[[DefinedTerm/mentorscript]], [[DefinedTerm/agents-md]], [[DefinedTerm/structured-agentic-software-engineering]]
