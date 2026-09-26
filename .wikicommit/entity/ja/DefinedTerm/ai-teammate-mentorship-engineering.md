---
title: "AI Teammate Mentorship Engineering（ATME）"
type: "schema:DefinedTerm"
lang: ja
tags: [SASE]
translated_from: ".wikicommit/entity/en/DefinedTerm/ai-teammate-mentorship-engineering.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Structured Agentic Software Engineering（SASE）で提唱されている、エージェント向けのプロジェクトの規範とベストプラクティスを、バージョン管理された MentorScript による「mentorship-as-code」として体系化するためのエンジニアリング活動。これにより指導は、暗黙的で一時的なものではなく、永続的で監査可能なものになる。"
---

AI Teammate Mentorship Engineering（ATME）は、[[DefinedTerm/structured-agentic-software-engineering]]（SASE）の一部として [[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で提唱されている構造化されたエンジニアリング活動の 1 つである。その目的は、エージェントへの指導を第一級のコードとして扱うこと、すなわち同論文が「mentorship-as-code」と呼ぶものによって、エージェントが生成したコードが単に機能するだけでなく、保守可能でチームの文化に沿ったものになるようにすることだとされている。

## 用法

同論文は ATME のもとでの指導を人間のコーチに割り当て、それをエージェントが永続的に取り込むものとしている。ルールは [[DefinedTerm/agent-command-environment]]（ACE）で作成され、[[DefinedTerm/agent-execution-environment]]（AEE）におけるエージェントの振る舞いに直接影響する。その成果物は [[DefinedTerm/mentorscript]] である。この活動に関する同論文の研究ロードマップは、次のものを求めている。微妙なニュアンスを含む指導を表現できるほど表現力が高く、それでいてチームが通常のエンジニアリング成果物としてレビューできるほど単純な抽象化。メンタリングのルールそのものの品質保証、すなわちリンティング、テスト、競合検出、回帰チェックであり、新しいルールが他の箇所に意図しない副作用を生まずにエージェントの振る舞いを改善することをどう検証するかの研究。そして、人間からの繰り返しのフィードバックからエージェントが候補となるルールを学習・説明しつつ、それらのルールをレビュー可能かつ監査可能に保ち、エージェントの判断を、それが考慮した具体的なルールに結びつける仕組み。

## 関連用語

[[DefinedTerm/mentorscript]]、[[DefinedTerm/agents-md]]、[[DefinedTerm/structured-agentic-software-engineering]]
