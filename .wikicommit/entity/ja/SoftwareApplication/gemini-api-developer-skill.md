---
title: "Gemini API 開発者スキル"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェントスキル, エージェントツーリング, コンテキストエンジニアリング]
translated_from: ".wikicommit/entity/en/SoftwareApplication/gemini-api-developer-skill.md"
source_commit: "a3e645ed9a2cca471e9bc76fd3ba0c25d255e24a"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Google が保守するエージェントスキル。コーディングエージェントに、Gemini API のモデル、SDK、ドキュメントの入口についての最新の知識を与える。"
  applicationCategory: "エージェントスキル"
  author: "[[Organization/google]]"
---

Gemini API 開発者スキル（`gemini-api-dev`）は、Google が github.com/google-gemini/gemini-skills で公開している [[DefinedTerm/agent-skills]] のパッケージである。Gemini API を扱うコーディングエージェントが、モデルの学習データのカットオフ時点で最新だったものではなく、Google の現行のモデルと SDK を使うように作られている。その作者らは、これをモデル開発者にしか提供できないものとしてではなく、このギャップに対してあらゆる SDK のメンテナーができることの一例として説明している。

## 機能

このスキルは、作者らが基本的なプリミティブ指示のセットと呼ぶものを提供する。API の高レベルな機能セットを説明し、各言語向けの現行のモデルと SDK を記述し、各 SDK の基本的なサンプルコードを示し、信頼できる情報源としてドキュメントの入口を列挙する。作者らはこれを、エージェントを最新のモデルと SDK へと導きつつ、ドキュメントも参照させるプリミティブな指示のセットと特徴付けており、それによって新しい情報がスキル自体から読み取られるだけでなく、信頼できる情報源から取得されるようにしている。

Google は、モデルのアップデートを出すのに合わせてこのスキルを保守し続けていると報告している。作者らは、この形式が抱える保守上の制約も挙げている。ユーザーに手動で更新してもらう以外に良い更新手段がなく、時間が経つにつれてユーザーのワークスペースに古いスキル情報が残りかねないと警告している。

## 導入とエコシステム

このスキルは GitHub から配布されており、Vercel skills または Context7 を通じてプロジェクトに直接インストールできる。

```
# Install with Vercel skills
npx skills add google-gemini/gemini-skills --skill gemini-api-dev --global

# Install with Context7 skills
npx ctx7 skills install /google-gemini/gemini-skills gemini-api-dev
```

Google は 117 のコード生成プロンプトから成る評価ハーネスでこのスキルを評価し、新しく推論能力の高いモデルでは結果が大幅に改善した一方、古いモデルでは改善がはるかに小さかったと報告している。数値と手法は [[BlogPosting/closing-the-knowledge-gap-with-agent-skills]] に示されている。
