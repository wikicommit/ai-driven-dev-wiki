---
title: "エージェント型ソフトウェアエンジニアリング：基盤となる柱と研究ロードマップ"
type: "schema:ScholarlyArticle"
lang: ja
tags: []
translated_from: ".wikicommit/entity/en/ScholarlyArticle/agentic-software-engineering-foundational-pillars.md"
source_commit: "1241f6026eea3b9fe7666601cd9fbf68d202989f"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "エージェント型ソフトウェアエンジニアリング（SE3.0）の時代に向けて、人間とエージェントそれぞれの専用ワークベンチ、バージョン管理されたアーティファクト、名前の付いたエンジニアリング活動から成るフレームワーク Structured Agentic Software Engineering（SASE）を、6 段階のエージェンシー／自律性の階層および研究ロードマップとともに提案する 2025 年のビジョン論文。"
  author: ["Ahmed E. Hassan", "Hao Li", "Dayi Lin", "Bram Adams", "Tse-Hsun Chen", "Yutaro Kashiwa", "Dong Qiu"]
  datePublished: "2025"
  keywords: ["エージェント型ソフトウェアエンジニアリング", "AI エージェント", "エージェント型 AI", "コーディングエージェント"]
---

「Agentic Software Engineering: Foundational Pillars and a Research Roadmap」は、Queen's University、
Concordia University、奈良先端科学技術大学院大学、Huawei Canada の研究者による 2025 年のビジョン論文で
ある。論文は、エージェント型ソフトウェアエンジニアリング（SE3.0）に必要なのは単により高性能な
エージェントではなく規律ある構造だと論じ、人間のための SE とエージェントのための SE という二重性を
導入して、その分割を軸にソフトウェアエンジニアリングのアクター、プロセス、ツール、アーティファクトを
再構想する。中心的な提案は [[DefinedTerm/structured-agentic-software-engineering]]（SASE）であり、
これは 2 つのモダリティのための専用環境、バージョン管理されたアーティファクト、名前の付いたエンジニア
リング活動から成る概念的な足場である。論文はまた、エージェンシーと自律性を区別する 6 段階の階層的
フレームワークを提案し、開発者がエージェントのチームを通じて 7 件のプルリクエストを解決する具体例に
議論を根拠づけ、最後に研究ロードマップとソフトウェアエンジニアリング教育への示唆についての議論で
締めくくっている。

## 要点

- [[DefinedTerm/structured-agentic-software-engineering]]（SASE）を提案し、ソフトウェアエンジニア
  リングの 4 つの柱 ― アクター、プロセス、ツール、アーティファクト ― を、人間のための SE（SE4H）と
  エージェントのための SE（SE4A）という二重性を軸に再構想する。
- [[DefinedTerm/se-autonomy-levels]] を導入する。これは SAE の自動運転の自動化レベルをモデルにした
  6 段階の階層（SE1.0–SE5.0）で、エージェンシー（計画を実行すること）と自律性（目標を策定すること）を
  区別する。
- 目的に特化した 2 つのワークベンチ ― 人間のコーチのための [[DefinedTerm/agent-command-environment]]
  （ACE）と、エージェントのための [[DefinedTerm/agent-execution-environment]]（AEE）― を定義し、両者を
  [[DefinedTerm/briefingscript]]、[[DefinedTerm/loopscript]]、[[DefinedTerm/mentorscript]] といった
  バージョン管理されたアーティファクトで接続する。
- SASE を運用可能にする 5 つの構造化されたエンジニアリング活動 ― [[DefinedTerm/briefing-engineering]]、
  [[DefinedTerm/agentic-loop-engineering]]、[[DefinedTerm/ai-teammate-mentorship-engineering]]、
  [[DefinedTerm/agentic-guidance-engineering]]、そして [[DefinedTerm/ai-teammate-lifecycle-engineering]]
  と [[DefinedTerm/ai-teammate-infrastructure-engineering]] を合わせた分野 ― を名づける。
- SWE-Bench 形式のベンチマーク結果に対する最近の監査が、エージェントが生成したコードはテストに合格
  してもマージ可能な水準に達しないことが多いと示していると報告し、GPT-4 のパッチの真の解決率が手動
  レビュー後に 12.47% から 3.97% に低下したといった知見を引用する。また、[[Dataset/swe-bench]] から、
  タスクの曖昧さと仕様不足に対処するために導入された [[Dataset/swe-bench-verified]]、そして汚染への
  懸念が高まるにつれて推奨されるようになった [[Dataset/swe-bench-pro]] への流れをたどる。
- GitHub 上で Claude Code の支援を受けたプルリクエストの 83.8% が最終的にマージされたとする初期の
  研究を引用し、エージェントが作成した 932,791 件のプルリクエストから成る [[Dataset/aidev]]
  データセットを、エージェント型コーディングがすでに広く普及していることの証拠として挙げる。

## 注記

論文は自らを決定的な解決策ではなく「概念的な足場」と位置づけ、提案した活動に異議を唱え、洗練し、拡張
するようコミュニティに明示的に呼びかけている。論文は SASE を関連する取り組み ― [[DefinedTerm/product-requirement-prompt]]
を用いる [[DefinedTerm/plan-do-assess-review]] ループ、エージェントスキルのプラグインライブラリ、
CLAUDE.md／AGENT.md のようなメタプロンプトファイル（[[DefinedTerm/agents-md]] を参照）、そして
[[SoftwareApplication/bmad]] マルチエージェントフレームワーク ― と比較し、SASE は「コードとしての
メンターシップ」、二重のワークベンチ、目標アーティファクトとしてのマージ可能性、そして第一級の
アーティファクトとしてのコンサルテーションによって差別化されると論じている。この論文は同じ著者らによる
以前の提案「Towards AI-Native Software Engineering (SE3.0)」を土台としており、その提案は論文自身の
参考文献に挙げられているが、ここでは分析していない。
