---
title: "Conductor"
type: "schema:SoftwareApplication"
lang: ja
tags: [マルチエージェント, オーケストレーション, エージェンティックコーディング, git worktree]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/conductor.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "Melty Labs による macOS 向けのローカルオーケストレータ。複数の Claude Code と Codex のエージェントを、それぞれ専用の git worktree で並行実行し、視覚的なダッシュボードと diff を軸としたレビューインターフェースを備える。"
  applicationCategory: "DeveloperApplication"
  author: "Melty Labs"
  operatingSystem: "macOS"
  softwareVersion: ""
  license: ""
---

Conductor は Melty Labs が作った macOS 向けのローカルなマルチエージェントオーケストレータである。複数の [[SoftwareApplication/claude-code]] と [[SoftwareApplication/codex]] のエージェントを並行実行し、それぞれに専用の git worktree を与え、diff を軸としたレビューインターフェースを備える視覚的なダッシュボードを通じて提示する。

## 概要

[[BlogPosting/the-code-agent-orchestra]] が2026年のツールの情勢に用いる3層の枠づけにおいて、Conductor は Tier 2——ローカルオーケストレータ——に位置する。そこでは開発者自身のマシンが隔離された worktree の中でエージェントを起動し、開発者はダッシュボード、diff のレビュー、マージの制御を通じてループの中に留まる。Osmani はこれを Mac 上でマルチエージェントオーケストレーションを始める最も速い方法だと記述し、その得意どころを、同じリポジトリ上の3〜8個の並行する機能を視覚的に監督することだと名指している。

## 機能

複数の Claude Code と Codex のエージェントの並行実行、エージェント1つにつき1つの git worktree、進行中の作業の視覚的なダッシュボード、そして diff を軸に構築されたレビューインターフェース。ふだんなら少数のシェルのエイリアスで済ませる worktree のライフサイクルの作業——worktree とブランチの作成、エージェントの起動、リベースと PR のオープン、終わった worktree の後片付け——が視覚的に扱われる。

## 沿革

ここで参照できる説明は、これが無償であり、ユーザーが払うのは自身の API のコストだけであること、そして今のところ macOS 専用で、Apple Silicon と Intel の双方のマシンに対応していることを述べている。
