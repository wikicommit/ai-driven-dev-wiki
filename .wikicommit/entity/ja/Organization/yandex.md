---
title: "Yandex"
type: "schema:Organization"
lang: ja
tags: [業界]
review_status: pending
translated_from: ".wikicommit/entity/en/Organization/yandex.md"
source_commit: "f06be6ff6feaf095ffb8e7a4ce28dc6471758c20"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "ロシアに拠点を置く企業。社内の Yandex Infrastructure チームが社内で使われる開発プラットフォームを構築し、そこから Yandex Code Assistant などの AI コーディング製品を生み出している。"
  foundingDate: "1997-09-23"
  url: "http://www.ya.ru/"
---

Yandex はロシアに拠点を置く企業である。この wiki では、まず自社の開発者に使われた AI コーディングツールの開発元として登場する。ここで参照できる記述はいずれも同社自身のエンジニアリングブログに由来するため、外部からの評価ではなく、同社が自らの取り組みをどのように提示しているかを述べたものである。

同社の Yandex Infrastructure チームは、社内の開発者が作業する基盤となるプラットフォームを構築している。後の投稿では、このチームは Yandex 社内でアプリケーションやサービスを作成・デプロイするためのツールを開発し、同社の開発者の大半が使うインフラストラクチャを支えていると説明されている。そのチーム内の ML ラボが開発したのが [[SoftwareApplication/yandex-code-assistant]] である。これはインラインでコードを提案するアシスタントで、社内で展開された後、Yandex Cloud プラットフォーム上で無料テスト向けに公開された。

## 沿革

同社のブログに付属する企業プロフィールでは、設立日は 1997 年 9 月 23 日とされている。

## 活動と製品

[[BlogPosting/how-we-taught-yandex-code-assistant-to-make-developers-happy]] によれば、このコードアシスタントは A/B テストで評価された。同投稿は A/B テストを Yandex では慣例的なものとしている。また、Yandex 社内でのアシスタントの利用が強制されたことは一度もなく、気に入らない開発者はプラグインを削除するだけでよかった。

SourceCraft の開発者ツールチームは、後の投稿によればその系譜を Yandex Infrastructure に置くチームで、2024 年 1 月に開発作業を開始し、その後 [[SoftwareApplication/vibecraft]] を構築した。これはコードを書かずにチャットからアプリケーションを作成するためのプラットフォームで、プログラミングを専門としない人々を対象としている。[[BlogPosting/programming-for-those-who-dont-write-code-how-vibecraft-works]] の説明によれば、VibeCraft は同社独自のスタック上で動作する。コードは SourceCraft のリポジトリに保管され、プロダクトはデータをサーバーレス YDB に置いて Yandex Cloud にデプロイされ、生成には Yandex 独自のモデルのアンサンブルが使われる。
