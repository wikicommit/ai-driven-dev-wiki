---
title: "DeepWiki"
type: "schema:SoftwareApplication"
lang: ja
tags: [コーディングエージェント, ドキュメント, コードベース理解]
review_status: pending
translated_from: ".wikicommit/entity/en/SoftwareApplication/deepwiki.md"
source_commit: "20326ae2b2d3074fa7e5e75e7d6a666eb50f9daf"
translated_at: "2026-09-27"
translated_by: "claude-opus-5-5"
translated_with: "0.8.0"

properties:
  description: "Cognition のコーディングエージェント Devin に付随する、コードベース向けのドキュメント生成機能。Devin がリポジトリにオンボードする際に、システム図を含む包括的で常に更新され続けるドキュメントを生成する。Cognition はこれを Devin のコードベース理解を目に見える形にしたものとして位置づけている。"
  applicationCategory: "コードベースのドキュメント生成ツール"
  author: "[[Organization/cognition]]"
---

DeepWiki は、Cognition が自社のコーディングエージェント [[SoftwareApplication/devin]] に結びつけている
ドキュメント機能である。Cognition の説明によれば、Devin はコードベースにオンボードする際に、システム図を含む
包括的で常に更新され続けるドキュメントを生成し、DeepWiki はそのドキュメントが提供される際の名称である。
Cognition はこれをエージェントを試すための単独の手段としても提示しており、
[[BlogPosting/devins-2025-performance-review]] の読者に対して、自分のコードベースの 1 つで DeepWiki を実行し、
Devin のコードベース理解を自ら確かめてみるよう勧めている。

## 機能

Cognition は DeepWiki を、Devin の「オンデマンドのシニアインテリジェンス（senior intelligence on demand）」と
呼ぶもの、つまりチケットの実行ではなく大規模なコードベースの理解に関わるエージェントの作業の一部として位置づけている。
同社によれば DeepWiki は大規模なリポジトリでも機能し、顧客はこれを使って 500 万行の COBOL や
500 GB のリポジトリのドキュメントを生成してきた。記事で説明されている計画ワークフローでは、エンジニアは
このドキュメントを読んだうえで Devin とチャットしてシステムを理解し、その後で作業の範囲を定める。

## 採用とエコシステム

Cognition が挙げる採用事例は、ある銀行のものである。同社によれば、Devin が 40 万以上のリポジトリにわたって
ドキュメントを生成したことで、この銀行は複数のエンジニアリングチームを大規模なドキュメント作成プロジェクトから外し、
新機能の開発に振り向けることができた。これはベンダーによる顧客成果の報告である。
