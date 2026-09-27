---
title: "Yandex Code Assistant"
type: "schema:SoftwareApplication"
lang: ja
tags: [コード補完, コーディングツール]
translated_from: ".wikicommit/entity/en/SoftwareApplication/yandex-code-assistant.md"
source_commit: "f06be6ff6feaf095ffb8e7a4ce28dc6471758c20"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "IDE 内でのインラインのコード提案に注力した Yandex のコードアシスタント。Yandex Infrastructure の ML ラボが開発し、Yandex Cloud プラットフォーム上で無料テスト向けに公開された。"
  applicationCategory: "AI コードアシスタント"
  author: "[[Organization/yandex]]"
---

Yandex Code Assistant は、Yandex Infrastructure の ML ラボが開発したコード作成アシスタントである。Yandex Infrastructure は、同社の開発者自身が日々の作業に使うプラットフォームを構築する Yandex のチームである。[[BlogPosting/how-we-taught-yandex-code-assistant-to-make-developers-happy]] によれば、このアシスタントは Yandex 社内のチームへのインライン提案の展開として始まり、その後 Yandex Cloud プラットフォーム上でテストモードとして無料で利用できる形で公開された。

この製品はチャットインターフェースではなく、あえてインライン提案、すなわち開発者の入力に合わせてグレーで表示され、Tab で受け入れ、Esc で却下するコードに注力している。チームは自分たちの経験を振り返り、同業の開発者と話した結果、実際に求められているのはインライン提案だと判断し、そこに注力することを選んだ。

## 機能

提案はテキストの任意の続きとしてではなく、抽象構文木によって特定される完全なコード文として生成される。文を途中で切ってしまう提案は悪い提案とみなされ、モデルは何も提案しないという選択もできる。モデルは既存のモデルを Yandex 自身のコードでファインチューニングしたもので、fill-in-the-middle に対応しているため、カーソルの前後両方のコードを考慮した提案ができる。記事は、ファインチューニングの対象言語として Python、TypeScript、C++、YAML、JSON、Kotlin、Java、Go、Swift、Scala、YQL/SQL を挙げている。

サービスは、すべてのビジネスロジックを担う CPU バックエンドと、推論を行う GPU バックエンドに分かれている。CPU バックエンドは、そもそも提案をリクエストするかどうかの判断、ユーザー自身のコードによるコンテキストの補強、しきい値に照らしたモデルの回答のランク付けを担う。JetBrains 系 IDE 向けのものを含む IDE プラグインは、プロキシとしてのみ機能する。レイテンシの目標は 500 ミリ秒とされ、記事は 99 パーセンタイルで 420 ミリ秒を報告している。

## 導入とエコシステム

Yandex 社内での利用は任意であり、チームは品質をリテンション、オフラインのユニットテスト指標、受け入れ率、そして最終的には複合指標である [[DefinedTerm/developer-happiness-metric]] によって評価した。同記事で示された Yandex 自身の数値によれば、開発者が 1 日に書くコードの 15% がアシスタントを使って書かれており、アシスタントを試した数千人の Yandex の開発者のうち 60% が常用ユーザーになった。
