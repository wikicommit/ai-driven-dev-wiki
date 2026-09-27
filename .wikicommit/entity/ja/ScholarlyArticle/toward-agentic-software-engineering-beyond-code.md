---
title: "コードを超えたエージェント型ソフトウェアエンジニアリングに向けて：ビジョン、価値、語彙の枠組み"
type: "schema:ScholarlyArticle"
lang: ja
tags: []
review_status: pending
translated_from: ".wikicommit/entity/en/ScholarlyArticle/toward-agentic-software-engineering-beyond-code.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "ICSE 2026 の AGENT ワークショップに採択されたポジションペーパー。エージェント型ソフトウェアエンジニアリングの研究は、コード中心の活動を超えて、ソフトウェアエンジニアリングのライフサイクル全体にわたる「プロセス全体」ビジョンへと拡張されるべきだと論じ、暫定的な CRAFT の価値と原則を提案するとともに、エージェント型 SE の語彙を設計するための指針を示している。"
  author: ["Rashina Hoda"]
  abstract: "本論文は、エージェント型 AI がソフトウェアエンジニアリングに激震のようなパラダイムシフトをもたらそうとしていると論じる。エージェント型 SE の初期のビジョンは主にコード関連の活動に焦点を当てているが、初期の実証的エビデンスは、より幅広い社会技術的な活動や関心事を考慮する必要があることを示している。本論文の貢献は、SE の基盤と進化に根ざした「プロセス全体」ビジョンに向けて、エージェント型 SE の範囲をコードの先へと拡張すること、コミュニティの取り組みを導く暫定的な価値と原則の集合、そしてエージェント型 SE のための明確に定義された語彙の設計と使用に関する指針である。"
  keywords: ["エージェント型ソフトウェアエンジニアリング", "プロセス", "ビジョン", "価値", "原則", "語彙", "用語", "エージェント型 AI"]
---

「Toward Agentic Software Engineering Beyond Code: Framing Vision, Values, and Vocabulary」は、Rashina Hoda によるポジションペーパーで、International Conference on Software Engineering（ICSE）2026 の AGENT ワークショップに採択された。エージェント型ソフトウェアエンジニアリング（SE）とは、SWE-agent、Google の Jules、OpenAI の Codex、Cognition の Devin、AutoCodeRover、Anthropic の [[SoftwareApplication/claude-code]] といった自律型 AI エージェントを使ってソフトウェアエンジニアリングの作業を遂行することを指す。本論文は、その初期のビジョンが主にコーディング関連の活動（生成、レビュー、デバッグ、修復、設定）に焦点を当ててきたと指摘し、エージェント型 SE が単なるコーディングの加速装置ではなく、プロセスレベルでの真のパラダイムシフトとなるためには、その範囲を SE のライフサイクル全体とその社会技術的な関心事にまで広げなければならないと主張する。

本論文はこの主張を、SE 自身の歴史的な進化の振り返りに基づけている。ウォーターフォール、スパイラル、V モデルからラショナル統一プロセス（RUP）を経て、アジャイル、リーン／カンバン、DevOps に至るまで、これら従来の SE プロセスモデルはいずれも、単一の活動ではなく、役割・プラクティス・成果物にまたがる「プロセス全体」のアプローチをとっていたと観察している。さらに、新たに登場しつつあるエージェント型 SE のフレームワークを概観している。具体的には、Roychoudhury らが提案した「agentic AI Software Engineer」という役割、Applis らが提案した統合ソフトウェアエンジニアリングエージェント（[[SoftwareApplication/useagent]]）、[[ScholarlyArticle/agentic-software-engineering-foundational-pillars]] で提案された [[DefinedTerm/structured-agentic-software-engineering]]（SASE）、そしてエージェント型プルリクエストのデータセット [[Dataset/aidev]] である。そのうえで、初期の実証研究が、チームワーク、協調、アカウンタビリティ、文化への対処におけるエージェント型 AI の限界を報告していること、また組織への導入の課題や人間と AI の協働に関する懸念が別途提起されていることに触れている。

この土台の上に、本論文は 3 つの貢献を示す。エージェント型 SE のための暫定的な [[DefinedTerm/whole-of-process-vision]]（SE のライフサイクル全体に及び、倫理的整合を新たな第一級の領域として導入する）、コミュニティの研究と実践を導く [[DefinedTerm/craft-values-and-principles]]（Comprehensive、Responsible、Adaptive、Foundational、Translational）、そしてエージェント型 SE の用語を設計するための [[DefinedTerm/agentic-se-vocabulary-considerations]] である。

## 要点

- エージェント型 SE には、コーディングだけを中心にとどまるのではなく、倫理的整合（Ethical Alignment）、要求工学（Requirements Engineering）、設計（Design）、開発（Development）、運用（Operations）という 5 つの上位領域にまたがる [[DefinedTerm/whole-of-process-vision]] が必要だと提案する。これらの領域には、人間とエージェントのアクターが、人間が制御するさまざまなレベルの AI エージェンシーのもとで反復的に取り組む。
- エージェント型 SE の研究と実践を方向づけるものとして、暫定的な [[DefinedTerm/craft-values-and-principles]]、すなわち Comprehensive（包括的）、Responsible（責任ある）、Adaptive（適応的）、Foundational（基盤的）、Translational（橋渡し的）（CRAFT）を提案する。各価値には 2 つの指導原則が対応づけられている。
- [[DefinedTerm/agentic-se-vocabulary-considerations]]（関連性、網羅性、受容性、一貫性、哲学的整合）を示し、分野が若いにもかかわらず、「agentic AI software engineer」「AI software engineer」「agentic software engineer」といった用語の間で、統語的・意味的なドリフトがすでに見られると指摘する。
- Roychoudhury らが記述した「agentic AI Software Engineer」という役割、Applis らが記述した [[SoftwareApplication/useagent]]、そして [[DefinedTerm/se-autonomy-levels]] の階層を伴う [[DefinedTerm/structured-agentic-software-engineering]] など、新たに登場しつつあるエージェント型 SE の提案を概観し、これらのビジョンは必要かつ歓迎すべきものではあるものの、依然として主に 1 つの SE 活動、すなわちコーディングに焦点を当てていると観察している。
- AI はコーディング、執筆、ドキュメント作成のタスクにおいて「個人の加速装置」として機能するものの、チームワークの問題を解決することは示されておらず、協調、アカウンタビリティ、文化への影響はいまだ不明確であるという初期の実証的知見を引用している。また、現在の研究は組織への導入や人間と AI の協働を狭い範囲でしか扱っていないことが多いとも指摘している。

## 補足

本論文は、そのビジョン、価値、語彙に関する指針を暫定的かつ網羅的ではないものと位置づけており、決定版のエージェント型 SE プロセスモデルとしてではなく、コミュニティからのフィードバックと協働を促すことを明確に意図している。分野の最終的な姿は、エージェント型のリポジトリやフォーラムの縦断的研究と、エージェント型 SE チームを対象とした詳細な実証研究（インタビュー、サーベイ、実験）を通じて初めて明らかになるかもしれないと述べ、ウォーターフォールモデルの逐次的というイメージ自体も、それが実際にどう使われたかから生まれたことになぞらえている。
