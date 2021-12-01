---
title: "セキュリティ・キャンプ全国大会2020に参加してきた<2>"
date: 2021-12-01T23:51:30+09:00
description: seccamp 全国大会2020の参加録（後編）
hideToc: false
enableToc: true
enableTocContent: false
author: Takana Norimasa
draft: true

tags:
- 参加録
- seccamp
categories:
- event
---

### seccamp閉会式〜12/24
期間内にセルフホストが出来なかった悔しさでモチベーションはseccampが終わったあとでも充分保たれていた．
受験生[^1]だし（は？）SECCON電脳会議の準備もあったが，コツコツ進めていった．（今考えたらなんでこの時期にCコンパイラをワーって開発していたのか謎だな）

発表前の最終週からガチャガチャとデバッグをしていたが，これでは埒が明かない気がしたので@hsjoihs氏からテストをもらった．
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">自作Cコンパイラやってる人、テストケースが追加でほしければ私のリポジトリのを使ってもらって構いませんよと書いておいた<a href="https://t.co/Tz6PIDHj4j">https://t.co/Tz6PIDHj4j</a></p>&mdash; hsjoihs (@hsjoihs) <a href="https://twitter.com/hsjoihs/status/1332833830378504193?ref_src=twsrc%5Etfw">November 28, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

これ，マジで最高なので自作Cコンパイラやってる人は取り入れたほうが良い．
テストでバグを潰しつつ，フランケン・コンパイルにおける自分のソースコードの割合を少しずつ増やしていった．

[^1]:大学受験ではない．

ここでせっかくなので，セルフホストに向けて何をやったかを具体的に話したい．
基本的にはRuiさんのcompilerbookに沿って実装を進めれば良いが，セルフホストにはまた別のノウハウが必要だからだ．[^2]

まず立ちはだかる問題として， **「どうやってセルフホストが成功したかを確かめるか？」** というものがある．

セルフホストのデバッグで何が辛いかと言うと，バグを見つけたとしてそれがどこに起因しているかパッと見分からないというものがある．

[^2]:そしてこれが具体的に書かれてる記事をあんまり見たことがない．

