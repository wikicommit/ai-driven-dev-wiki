---
title: "エージェント型エンジニアリングのパターン"
type: "schema:CreativeWorkSeries"
lang: ja
tags: [エージェント型エンジニアリング, コーディングエージェント, デザインパターン]
translated_from: ".wikicommit/entity/en/CreativeWorkSeries/agentic-engineering-patterns.md"
source_commit: "d3a6cc04042ea62012d6cdb8d9075c83b708d517"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"
review_status: pending

properties:
  description: "Simon Willison が 2026 年 2 月に書き始めた、章立て形式のガイド。コーディングエージェントから最良の結果を引き出すためのパターンを集めている。各章は、初出の時点で固定されるのではなく、時間とともに更新されていくよう設計された形式で公開されている。"
  about: "[[DefinedTerm/agentic-engineering]]"
  author: ["Simon Willison"]
  url: "https://simonwillison.net/guides/agentic-engineering-patterns/"
  startDate: "2026-02-23"
  creativeWorkStatus: "章の追加が続いている。ガイド自身は作業途中のものだと述べている"
---

Agentic Engineering Patterns（エージェント型エンジニアリングのパターン）は、Claude Code や OpenAI Codex
といったコーディングエージェントから最良の結果を引き出すためのプラクティスを集めたもので、2026 年 2 月から
Simon Willison のブログで公開されている。一連の章として構成されており、各章はそれぞれ独立した 1 つのパターン
である。これを紹介した投稿では、その目的を、「どうすればこれで良い結果を得られるのか」という問いに答える助けと
なるものを 1 か所にまとめて作ることだと述べている。その背景には、AI 支援型プログラミングについて著者がこれまで
書いてきた文章があり、彼はそれを比較的まとまりのないものだと評している。

著者が新しいと考えているのは、その形式の部分である。彼はこのコレクションを、厳密には本ではないが「本のような
形をしたもの」と表現し、自身が *ガイド* と呼ぶコンテンツの形で公開している。ガイドとは章の集まりであり、章は
実質的に日付の目立たないブログ投稿であって、初出の時点で固定されるのではなく、時間とともに更新されていくよう
設計されている。彼はガイドと章を、ブログ上でエバーグリーンなコンテンツを公開するという、しばらく前から解決
しようとしてきたと自ら述べる問題への答えとして提示している。単一の公開イベントではなくこの形式こそが、この
コレクションがここでシリーズとして記録されている理由である。

本作が影響を受けたと明言しているのは、1990 年代のソフトウェアのデザインパターン文献によって広まった、章立ての
パターン形式である。紹介投稿はこれを、厳密に従ったモデルではなく、緩やかなインスピレーションだと説明している。
プロジェクトを紹介した投稿については [[BlogPosting/writing-about-agentic-engineering-patterns]] を参照。

## 範囲と構成

ガイドの章は 6 つの見出しのもとにまとめられている。**原則**（Principles）には「エージェント型エンジニアリング
とは何か」（What is agentic engineering?）、「コードを書くのは今や安い」（Writing code is cheap now）、
「やり方を知っていることを蓄えておく」（Hoard things you know how to do）、「AI はより良いコードを生み出す
助けになるべきだ」（AI should help us produce better code）、「アンチパターン：避けるべきこと」
（Anti-patterns: things to avoid）が含まれる。**コーディングエージェントとの協働**（Working with coding
agents）には「コーディングエージェントの仕組み」（How coding agents work）、「コーディングエージェントと
Git を使う」（Using Git with coding agents）、「サブエージェント」（Subagents）が含まれる。**テストと QA**
（Testing and QA）には「Red/Green TDD」（Red/green TDD）、「まずテストを実行する」（First run the tests）、
「エージェント型の手動テスト」（Agentic manual testing）が含まれる。**コードの理解**（Understanding code）
には「線形ウォークスルー」（Linear walkthroughs）と「インタラクティブな説明」（Interactive explanations）が
含まれる。**注釈付きプロンプト**（Annotated prompts）には 2 つの実例が収められ、**付録**（Appendix）には
著者が繰り返し使うプロンプトが集められている。

プロジェクトは、告知と同時に公開された 2 つの章 — 「コードを書くのは今や安い」と「Red/Green TDD」 — から
始まり、想定する更新ペースは週に 1〜2 章だと述べられていた。著者は、扱うべきことが多いので、いつやめるのかは
自分でもよくわからないと語っている。

## ステータス

ガイドの冒頭の章は、このプロジェクトを、それが扱おうとしている分野と同様に、まさに作業途中のものだと説明し、
どの章も完成したものとは見なすべきでないと述べている。著者は、新しい手法が現れるにつれて章を追加し続け、
パターンについての理解が深まるにつれて既存の章を更新していくと述べている。そこで掲げられている編集上の目標は、
これらのツールを使って作業するためのパターンのうち、実証的に成果を上げ、ツールが進歩しても古びにくいものを
特定し、記述することである。

掲げられている編集上の制約は、文章は生成されたものではなく著者自身が書くということである。彼は AI が生成した
文章を自分の名前で公開しないという強い個人的方針を持っており、このプロジェクトでもそれを守ると述べている。
一方で、校正、サンプルコードの肉付け、その他の周辺作業には LLM を使っている。

## 関連

[[DefinedTerm/agentic-engineering]]、[[DefinedTerm/ai-coding-agent]]、[[DefinedTerm/vibe-coding]]、
[[BlogPosting/writing-about-agentic-engineering-patterns]]
