---
title: "自作Cコンパイラセルフホストへの道"
date: 2022-03-05T21:04:44+09:00
description: 輪読会で発表した資料
hideToc: false
enableToc: true
enableTocContent: false
author: n.takana

tags:
- C compiler
categories:
- tech
draft: true
---

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vRdktxPg6QFMNYsHxO5GtedIBoRCDaREdz1gkUmccTq9T0lPlGNYaDttxqWYZPX5uJJ2IsZiZ2LoK_U/embed?start=false&loop=false&delayms=3000" frameborder="0" width="1440" height="839" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

Ruiさんの[低レイヤを知りたい人のためのCコンパイラ作成入門](https://www.sigbus.info/compilerbook)の輪読回で喋った資料．
この輪読回はミニキャンプ2021で僕がチューターを担当したグループワークが主催しているもので，素晴らしいことに現在も続いている．
僕も（忘れてない限り）毎回[^1]お邪魔させていただいてるのだが，部屋であんまり喋れなかったりして発表もせずにクネクネしてることが多いので今回こそはと資料を作った．[^2]

[^1]:じゃあ毎回じゃねぇじゃん
[^2]:正直に言うとこの記事を書いてる段階ではほとんど資料を作れてない（は？）

内容としては，まぁ上のスライドを見れば分かると思うが自作Cコンパイラのセルフホストまでのロードマップである．
やってる最中はガーッと実装しているので中々こういう資料が出回るのは少ないと思うが，やってる側としてはあとどんなことをやってどんな課題をクリアすればセルフホストなのか見えてこないと辛いんじゃないかなぁということで書いた．
特にRuiさんのcompiler bookは非常にわかりやすくて足がかりとして非常に重要なものだが，セルフホストまで行こうとするには自力で頑張るべき部分も多い．
あれを最後まで完走すれば実装する力は付いていると思うが，どっから取りかかれば良いか途方にくれる人も居ると思う．（自分も実際seccampで指導をいただかなかったらあの期間ではセルフホストまで行かなかっただろう）
ぜひこれを参考にセルフホストへの道を突き進んでくれたらと思う．

ちなみに[seccampの感想記事](https://alignof.github.io/blog/posts/seccamp/)の後編はまだあんまり書いていません...（小声）
セルフホストまでのことを書く一番大事な部分何だけどなぁ...
溜まってるブログネタ，どっかで放出しないとなぁ...（春休みの今以外にどこで放出する気なんだお前）

