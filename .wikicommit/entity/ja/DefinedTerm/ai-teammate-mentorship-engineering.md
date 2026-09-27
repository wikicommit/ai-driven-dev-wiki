---
title: "AI Teammate Mentorship Engineering（ATME）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/ai-teammate-mentorship-engineering.md"
source_commit: "f3cd768971749927e49083efe4fbd9f44cf27fb0"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Structured Agentic Software Engineering（SASE）で提案されている、プロジェクトの規範とベストプラクティスを、バージョン管理された MentorScript によってエージェント向けの「コードとしてのメンターシップ（mentorship-as-code）」として成文化し、指導を暗黙的で一過性のものではなく、永続的で監査可能なものにするためのエンジニアリング活動。"
---

AI Teammate Mentorship Engineering（ATME）は、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で提案されている構造化されたエンジニアリング活動の 1 つである。その目的として述べられているのは、エージェントに対する指導を第一級のコードとして扱うことで、エージェントが生成したコードが単に動作するだけでなく、保守可能でチームの文化にも沿ったものになるようにすることであり、同論文はこれを「コードとしてのメンターシップ（mentorship-as-code）」と呼んでいる。

## 用法

同論文は、ATME のもとでの指導を人間のコーチの担当とし、それがエージェントによって永続的に消費されるものと位置づけている。ルールは [[DefinedTerm/agent-command-environment]]（ACE）で作成され、[[DefinedTerm/agent-execution-environment]]（AEE）におけるエージェントの振る舞いに直接影響する。この活動の成果物は [[DefinedTerm/mentorscript]] である。同論文がこの活動について示す研究ロードマップは、次のものを求めている。すなわち、きめ細かな指導を表現できるほど表現力がありながら、チームが通常のエンジニアリング成果物としてレビューできるほど簡潔な抽象化。メンターシップのルールそのものに対する品質保証（リンティング、テスト、衝突検出、回帰チェック）であり、新しいルールが他の箇所に意図しない副作用を生むことなくエージェントの振る舞いを改善することをどう検証するかの研究を含むもの。そして、人間からの繰り返しのフィードバックをもとにエージェントが候補となるルールを学習・説明しつつ、それらのルールをレビュー可能かつ監査可能に保ち、エージェントの判断をそれが考慮した特定のルールに結びつける仕組みである。

## 関連用語

[[DefinedTerm/mentorscript]], [[DefinedTerm/agents-md]], [[DefinedTerm/structured-agentic-software-engineering]]
