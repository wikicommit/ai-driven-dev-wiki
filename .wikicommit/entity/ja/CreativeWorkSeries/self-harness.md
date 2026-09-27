---
title: "self-harness"
type: "schema:CreativeWorkSeries"
lang: ja
tags: [エージェント, エージェントアーキテクチャ, コンテキストエンジニアリング, エージェント型エンジニアリング]
translated_from: ".wikicommit/entity/en/CreativeWorkSeries/self-harness.md"
source_commit: "c6b8c68a8b3e34ab51b855aeb44d0daa53497505"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  about: "[[DefinedTerm/harness-engineering]]"
  author: "Datawhale"
  url: "https://datawhalechina.github.io/self-harness/"
  creativeWorkStatus: "アルファ版"
---

self-harness は、[[DefinedTerm/harness-engineering]] に関するオープンソースの中国語チュートリアルであり、
Datawhale コミュニティによって、番号付きの章のシリーズと付随する実践プロジェクトとして公開されている。
その目的として掲げられているのは、複雑で長時間稼働する AI エージェントのための堅牢な基盤ランタイム
アーキテクチャをどう構築するかを、開発者が理解できるよう支援することである。

このシリーズは、この分野を互いに代替し合う手法の集まりとしてではなく、段階的な発展として整理している。
すなわち、[[DefinedTerm/prompt-engineering]] から、動的な情報管理としての
[[DefinedTerm/context-engineering]] を経て、システムレベルのハーネスエンジニアリングへと至る、という流れで
ある。この枠組みはチュートリアル自身の構成上の主張であり、各章が従う順序を与えている。

想定読者は、AI アプリケーション開発者、大規模モデル技術に関心のある人、そして基本的なプログラミング能力を持つ
Python 開発者である。読者が得られる成果として挙げられているのは、コンテキストエンジニアリングがプロンプト
エンジニアリングとどう異なるかを理解すること、動的なコンテキスト管理を扱えるようになること、拡張可能な AI
スキルシステムを設計すること、そして [[SoftwareApplication/claude-code]] に代表される種類の最小限のシステムを
構築することである。

## 範囲と構成

チュートリアルは理論編と実践編に分かれている。理論編の章では、プロンプトエンジニアリングの概念・手法・限界、
コンテキストエンジニアリングの概念と手法、長時間にわたって破綻せずに動き続けなければならないエージェントのための
ハーネス設計、そしてこの 3 つをつなぐ発展の流れを紹介する。実践編は [[SoftwareApplication/minimaster]] を軸に
構成されている。これは最小限のハーネス実装であり、そのコードは同じリポジトリに同梱されている。チュートリアルは
これを使って、ハーネスの理論が実際のエージェントシステムにどう落とし込まれるかを示している。

シリーズは <https://datawhalechina.github.io/self-harness/> でオンライン閲覧でき、各章は実践用のコードと並んで
Markdown としてリポジトリに置かれている。

## ステータス

プロジェクトはアルファ版とされている。プロジェクト自身の告知では、内容はまだ改善中であり誤りや漏れを含む可能性が
あると述べ、読者に Issue の登録を呼びかけている。リポジトリの未完了作業リストには 1 つの項目が挙げられている。
主流のハーネスシステム上に構築されたエージェント製品の分析であり、その例として NanoBot と OpenHarness が
挙げられている。

この作品のライセンスは、クリエイティブ・コモンズ 表示 - 非営利 - 継承 4.0 国際（CC BY-NC-SA 4.0）である。
