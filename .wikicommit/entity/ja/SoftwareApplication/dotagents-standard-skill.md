---
title: "dotagents-standard"
type: "schema:SoftwareApplication"
lang: ja
tags: [エージェントスキル, コンテキストエンジニアリング, 段階的開示]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/dotagents-standard-skill.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "dotagents のルーター／ライブラリの規約をエージェントに適用させるためのエージェントスキル。新規の .agents/ レイアウトの構築、肥大化したコンテキストファイルのそこへの移行、あるいは既存のものを読み過ぎずに辿ることを扱う。"
  applicationCategory: "DeveloperApplication"
  author: "Jeff Mixon"
  operatingSystem: ""
  softwareVersion: ""
  license: "MIT"
---

`dotagents-standard` は [[DefinedTerm/dotagents]] の規約をパッケージ化した [[DefinedTerm/agent-skills|エージェントスキル]] であり、エージェントがプロジェクトごとに教え直されることなくそれを適用できるようにする。作者が述べる空白は、規約それ自体は読むのは早いが適用するのが難しい、というものだった。標準はコンテキストを種類ごとに分けるべきだと述べるが、ある段落がどの種類に属するかは述べない。この分類のステップこそ、このスキルが供給するものである。

## 概要

3つの状況で起動する。新規の `.agents/` レイアウトを構築するとき、肥大化した `AGENTS.md`、`CLAUDE.md`、`.cursorrules` をそこへ移行するとき、そしてすでにそれを持つリポジトリの内側で作業しつつ、読み過ぎずに辿る必要があるときである。

## 機能

このスキルは [[DefinedTerm/progressive-disclosure]] を自らの素材に適用している。`SKILL.md` は1画面ぶんに留まり、心的モデル、分類のタクソノミーの表、2つのワークフロー——既存の構成を*活用（Utilize）*するものと、新しいものを*実装（Implement）*するもの——そしてルーターのパターンを保持する。より深い素材は `references/` ディレクトリに置かれる。1つはサブディレクトリごとに詳しく踏み込み、もう1つはより広い `.agents` Protocol の上位集合を扱い、いずれもタスクがその深さを必要とするときにだけ読まれる。`assets/templates/` ディレクトリはルーターファイル、ルールファイル、決定のメモリファイル、ペルソナ、スキルのコピー＆ペースト用の雛形を保持し、`examples/sample-project/` ディレクトリは、空白のテンプレートに対応する具体物として、架空の課金 API 向けに完全に書き込まれたレイアウトを保持する。

ルーターの規則についての指針は、それぞれがトリガーを名指し、動作の動詞——`READ`、`CHECK`、`CONSULT`、`ADOPT`、`RUN`——を携えること、というものである。そうすればポインタは、エージェントに何をすべきか、どういう条件のもとでかを伝える。

## 沿革

インストールは `npx skills add zaventh/dotagents-standard-skill` であり、投稿によれば agentskills.io 互換のあらゆるエージェントで機能し、同じ CLI の check と update のコマンドで最新に保たれる。[[SoftwareApplication/claude-code]] に限れば、ユーザーのスキルディレクトリへのシンボリックリンクでも機能する。MIT ライセンスであり、CI がプッシュのたびにスキル自身のフロントマターを検証し、すべての参照のリンクをチェックする——作者はこれを、この成果物が他のリポジトリに求めるのと同じ水準を自らに課しているものとして枠づけている。
