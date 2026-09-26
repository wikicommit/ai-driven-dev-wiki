---
title: "Twelve-Factor Agentic SDLC"
type: "schema:DefinedTerm"
lang: ja
aliases: ["Agentic SDLC 12 Factors", "12-Factor Agentic SDLC"]
tags: [エージェント型エンジニアリング, SDLC, 方法論, 仕様駆動開発]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/twelve-factor-agentic-sdlc.md"
source_commit: "b5ca703338b47ee427f9fd85de1f456b7453f357"
translated_at: "2026-09-26"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "tikalk/agentic-sdlc-12-factors リポジトリで公開されている、AI コーディングエージェントをソフトウェア開発ライフサイクル全体を通じた不可欠な参加者としてソフトウェアを構築するための方法論。マインドセット、コンテキスト、仕様化と計画、実行、レビュー、テスト、トレーサビリティ、ツーリング、ディレクティブ、チームの能力を扱う 12 のファクターとして記述されている。"
---

Twelve-Factor Agentic SDLC は、AI コーディングエージェントをソフトウェア開発ライフサイクル全体を通じた不可欠な参加者として、ソフトウェアを構築するための方法論である。そのリポジトリはこれを、AI 支援によるソフトウェア開発に向けて開発プロセスを最適化するフレームワークであり、保守性、スケーラビリティ、そして人間と AI の効果的な協働を重視するものだと説明している。また、AI 支援開発を導入し拡大してきたチームの実体験から抽出したベストプラクティスを統合したものだとしている。想定読者は、AI の支援を受けてアプリケーションを構築する開発者、運用エンジニア、エージェント型のプラクティスを導入する開発チーム、そして AI による変革を導く技術リーダーである。本文は Creative Commons 表示-継承 4.0 ライセンスの下で公開されており、別途ウェブサイト版もある。

## 用法

リポジトリは 12 のファクターを次のように記述している。

1. **Strategic Mindset（戦略的マインドセット）** — AI を、明確な指示、指導、厳密なレビューを必要とする、速くて知識豊富なジュニアパートナーとして扱う。
2. **Context Scaffolding（コンテキストの足場づくり）** — すべてのコンテキスト（コード、ドキュメント、チームの標準）を、重要なソフトウェアライブラリと同じ厳密さで管理する。
3. **Mission Definition（ミッションの定義）** — すべてのタスクを課題管理システム上の Mission Brief から始め、正式でバージョン管理された仕様（`spec.md`）を生成する。
4. **Structured Planning（構造化された計画）** — 仕様を使って AI 支援による実装計画（`plan.md`）を生成し、開発者がそれをレビューし、洗練し、優先順位を付ける。
5. **Dual Execution Loops（二重の実行ループ）** — 複雑な問題にはリアルタイムの同期的な協働を、明確に定義されたタスクには非同期の委任を使いこなす。
6. **The Great Filter（大いなるフィルター）** — 人間の開発者が品質の最終的な裁定者であり、すべての AI の出力を正しさ、アーキテクチャの一貫性、セキュリティ、センスの観点でふるいにかける。
7. **Adaptive Quality Gates（適応的な品質ゲート）** — 同期的な作業には継続的な「マイクロレビュー」を、非同期でエージェントが生成したすべてのコードには正式な「マクロレビュー」を行う。
8. **AI-Augmented, Risk-Based Testing（AI で拡張したリスクベースのテスト）** — 開発者がビジネス上およびセキュリティ上のリスクを定義し、AI がそれを検証する的を絞ったテストを生成する。
9. **Traceability（トレーサビリティ）** — 課題管理システム上のビジネス上の意図から、リポジトリ内の仕様とコードまでを自動的に結び付ける。
10. **Strategic Tooling（戦略的なツーリング）** — 専用ツールを中央のゲートウェイを通じて管理し、コスト、セキュリティ、モデルの選択を制御する。
11. **Directives as Code（コードとしてのディレクティブ）** — 再利用可能なルールや例からタスクの仕様に至るまで、すべての自然言語による指示をバージョン管理された資産として扱う。
12. **Team Capability（チームの能力）** — ベストプラクティスの共有を形式化し、バージョン管理された評価スイートでパフォーマンスを測定することで、組織としての身体知を築く。

この方法論は、同じ GitHub organization のツールで実装されている。[[SoftwareApplication/adlc-team-skills]] は Twelve-Factor Agentic SDLC を実装していると述べ、自身のスキルを個々のファクターに対応付けている。ミッションの定義はプロダクト系のスキルに、構造化された計画はアーキテクチャ系のスキルに、トレーサビリティはプロダクトとアーキテクチャの記録からコードまで追跡される意思決定に、コードとしてのディレクティブはバージョン管理されたディレクティブのライフサイクルに対応する。

2 つのリポジトリは、すべてのファクターを同じ名前で呼んでいるわけではない。ファクター III、IV、IX、XI は名前が一致するが、adlc-team-skills の対応表ではファクター VII を「Verification-First Evals」、VIII を「Ratchet Effect」、X を「Context Engineering」、XII を「Build to Delete」としており、方法論自身の一覧ではそれぞれ Adaptive Quality Gates、AI-Augmented Risk-Based Testing、Strategic Tooling、Team Capability となっている。どちらが新しい、あるいは正式な名称なのかは、情報源には書かれていない。

## 適用される場面

この方法論は、作業が課題管理システムから始まり、仕様がバージョン管理され、エージェントが生成するものすべてを人間がレビューするチームでの利用を前提としている。ファクター VI は人間の開発者を品質の最終的な裁定者とし、ファクター V は同期的なペアリングに向く作業と非同期に委任できる作業とを区別している。その位置づけは実務者による知見の統合であり、リポジトリはこれをチームの実体験から抽出したものとして提示し、コントリビューションを受け付けている。

## 関連用語

- [[DefinedTerm/spec-driven-development]] — 仕様を先に書く開発手法。ファクター III と IV は `spec.md` と `plan.md` を通じてこれを土台にしている
- [[DefinedTerm/context-engineering]] — adlc-team-skills の対応表がファクター X に付けている名前
- [[SoftwareApplication/agentic-sdlc-spec-kit]] — 同じ GitHub organization による仕様駆動開発のコマンドフレームワークで、adlc-team-skills はこれと共存するよう設計されている
