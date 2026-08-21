---
title: "理解負債"
type: "schema:DefinedTerm"
lang: ja
tags: [コード品質, 検証, AI 支援プログラミング, 用語]
review_status: pending
translated_from: ".wikicommit/entity/en/DefinedTerm/comprehension-debt.md"
source_commit: "94b85527dbced867228a76de4e40c1b535bfbc78"
translated_at: "2026-08-21"
translated_by: "claude-opus-5[1m]"

properties:
  description: "誰かがそれを理解するよりも速くコードがコードベースに入ってくるときに蓄積していく負債。説明できない挙動に対してチームが責任を負う状態を残す。"
  termCode: ""
  inDefinedTermSet: ""
---

理解負債とは、生成されたコードが、どの人間がそれを理解するよりも速くコードベースに入ってくるときに開く隔たりのことである。[[BlogPosting/survey-of-development-workflows-in-the-coding-agent-era]] はその根本原因を、生成速度と理解速度のあいだにある5倍から7倍の差だとし、これを通常の品質問題としてではなく、エージェント活用における成熟度を規定する失敗モードのひとつとして挙げている。

## 用法

このサーベイが示す例示は、Addy Osmani によるものとされる一人称の証言である。「テストは通った、ざっと目を通した、マージした、そして3日後には自分でもそれがどう動くのか説明できなかった」。また、AI の支援を使う開発者のあいだでスキル獲得が 17% 低下したという研究も伝えている。

そこで挙げられている対策は2つの半分からなる。第一に、エージェントに自分が生み出したコードの**線形なウォークスルー**を生成させること——このサーベイが Simon Willison に帰しているパターンである。第二に、人間が実際にそれを読んで理解するための時間を確保すること。これはツールの問題ではなくスケジューリングの決定である。

この用語についての締めくくりの観察は、皮肉なものだ。コードを書く者であることをやめて監督者になるためには、読む力はより重要でなくなるどころか、*より*重要になる。

## 関連用語

理解負債は [[DefinedTerm/verification-debt]] や [[DefinedTerm/verification-bottleneck]] と隣接しているが、指しているのは別の不足である——コードが正しさの観点で検査されずに済まされたということではなく、それが何をするのかについて誰も動く模型を築かなかった、ということだ。スキルの萎縮という側面は、この用語を [[DefinedTerm/productivity-reliability-paradox]] における開発者経験という調整変数へと結びつける。
