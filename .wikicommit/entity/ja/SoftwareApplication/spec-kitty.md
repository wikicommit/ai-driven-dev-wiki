---
title: "Spec Kitty"
type: "schema:SoftwareApplication"
lang: ja
tags: [仕様駆動開発, git worktree, コードレビュー, エージェンティックコーディング, フレームワーク]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/spec-kitty.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "コードエージェントを用いた仕様駆動開発のためのオープンソースのコマンドラインツール。仕様、計画、タスクをリポジトリの内側に保ち、レビューと受け入れのゲートの背後で、実装の作業を git worktree に隔離する。"
  applicationCategory: "DeveloperApplication"
  author: ""
  operatingSystem: ""
  softwareVersion: ""
  license: ""
---

Spec Kitty は、コードエージェントを用いた [[DefinedTerm/spec-driven-development]] のためのオープンソースのコマンドラインツールである。プロダクトの要求を反復可能なワークフローへ変え、仕様、計画、タスクを専用のディレクトリとしてリポジトリそのものの内側に保ち、git worktree を用いて実装の作業を隔離する。宣言されているフローは spec、plan、tasks、next、review、accept、merge の各ステップを辿り、Claude、Cursor、Gemini を含む複数のエージェントへの対応を掲げている。

## 概要

[[ScholarlyArticle/from-prompt-to-process]] の6次元のタクソノミーにおいて、Spec Kitty は仕様、役割、検証を覆い、その際立った特徴は実行にある。仕様・コンテキスト・役割・実行・検証・移植性にわたって 2, 1, 1, 2, 2, 1 を記録している——12点満点中9点であり、検討された6つのフレームワークのうち2番目に高く、実行で 2 を記録した唯一のものである。

## 機能

その評価において際立たせているのは worktree である。作業パッケージを隔離することで、エージェントが統制されたしかたで実装できるようにし、マージの前にレビューと受け入れを必須とする。論文はこれを、人間の統制点をフローへ挿入し、エージェンティックな開発を確立されたコードレビューの実践へ近づけるものと読み、同じ機能を、タクソノミーの各次元が分割ではなく重なり合うレンズであることの例示としても用いている——worktree による隔離は実行であり、マージ前に必須のレビューは検証である。

## 沿革

記録されている主な留保は設計ではなく浸透度である。論文は、この一群の他のフレームワークと比べてまだ控えめな採用状況を指摘し、Spec Kitty が浸透度のフィルタの閾値ぎりぎりで含められたと述べ、成熟度と採用を未解決の問いのままに残している。自身のリポジトリの規約と git worktree に依存していることも、複数エージェントへの対応にもかかわらず移植性が部分的と評価される理由として挙げられている。
