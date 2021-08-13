---
title: "セキュリティ・キャンプ全国大会2020に参加してきた"
date: 2020-12-31T01:31:30+09:00
description: seccamp 全国大会2020の参加録
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


## はじめに
修了してから結構経ってしまったが，seccampの参加録を書く．
~~もう1ヶ月位経つのか...~~（2021 8/7追記：こう書いてから受験とかのわちゃわちゃで今まで放置していた．俺って一体...）
もう1年くらい経つのか... 次のseccamp2021が始まっちゃってるよ...
とりあえず記憶とTwitterを頼りに書く．

参加した動機は去年度SecHack365に参加してアウトプットが多かったので，そろそろインプットが欲しかったのと技術だけで勝負なイベントに参加したくなったというのがあったりする．
他にもオンラインの代わりに今後の参加権を失わないで済むとかの条件は大きかった．
SecHackとseccampには一度参加しておきたかったイベントだったので両方体験できたのは良かったな...

## 振り返り
僕はCコンパイラを自作するY-Ⅲというコースに所属していた．
動機はC言語を長く触っていた（5年くらい．プログラムを書き始めたきっかけは苦しんで覚えるC言語のサイトを見たから）のと，SecHackの同期の方に結構Cコンパイラ自作をオススメされていてY-Ⅲを知る前からすでに自作Cコンパイラを書き始めていたから．
応募課題は開発途中のCコンパイラについて語っていた気がする．2日以上かけて書いた記憶．
応募締め切りを延長されたときには流石に焦った...[^1]

[^1]:何してくれんねんのお気持ち．

さておき，めでたく受かった．
合格を知ったのはSecHack365 Returnsの休憩時間だったのをよく覚えている．
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">テントとか買わないと... <a href="https://t.co/Ln1BSvrj4d">pic.twitter.com/Ln1BSvrj4d</a></p>&mdash; and rsp,-0x10 (@\_Alignof) <a href="https://twitter.com/_Alignof/status/1305023875638419461?ref_src=twsrc%5Etfw">September 13, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

### 合格から開始まで
受かったのが9/13らしいので始まるまでⅠヶ月ちょいあったことになる．
この間に何があったかというと，Twitter曰く「旅する海とアトリエ」の完結が決まってメンタルが終わってたりSecHack365 '19の成果発表会に出たりしてたらしい．
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">1週間ほどTypetalkに引きこもって廃人同様の生活を送っていたが改善の傾向は見られなかった．</p>&mdash; and rsp,-0x10 (@\_Alignof) <a href="https://twitter.com/_Alignof/status/1309376126976892929?ref_src=twsrc%5Etfw">September 25, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">このあと15時過ぎからLT枠で習慣化とかについてゆるく語ります．<br>お楽しみに．<a href="https://twitter.com/hashtag/SecHack365?src=hash&amp;ref_src=twsrc%5Etfw">#SecHack365</a> <a href="https://t.co/5gdPHvFYYf">https://t.co/5gdPHvFYYf</a></p>&mdash; and rsp,-0x10 (@\_Alignof) <a href="https://twitter.com/_Alignof/status/1309722658402041862?ref_src=twsrc%5Etfw">September 26, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
キャンプが始まるまでに構造体とか諸々を実装するつもりで，最終的にセルフホストまで行く気満々だった．
週報によると，9月2週に初期化式，9月3週に配列を実装，10月1週に配列のバグを修正し，10月2週にコードフォーマットの整理や仕様書の作成をしていた．
キャンプ前最後の1週間はインクリメントや文字リテラルまで実装が終わらせたが，構造体までは行かなかった．

### 開会式
開会式なるものがあった．
SecHack365で見知った顔が講師・受講者共にたくさんいて面白かった．（結構どっちも受けてる人は多いと思う）
普通の説明の他に講演があったのだが，結構ためになる話とかグレーな話があって良き．
LT大会もそうだがここでしか聞けない面白い話ってやつが多いと思う．
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">LT大会，美少女ばっかりで震えてる<a href="https://twitter.com/hashtag/seccamp?src=hash&amp;ref_src=twsrc%5Etfw">#seccamp</a></p>&mdash; and rsp,-0x10 (@\_Alignof) <a href="https://twitter.com/_Alignof/status/1317753504685981696?ref_src=twsrc%5Etfw">October 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
LT大会も全部聞きたいくらい良かったなぁ... 

「美少女になろう」って発表に知ってるオタクが大集合してたのが個人的ハイライト．（最悪）
なお，このあとはグループワークがありオタクくんが死亡した模様．
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">非テキストベースの会話苦手マン参上！</p>&mdash; and rsp,-0x10 (@\_Alignof) <a href="https://twitter.com/_Alignof/status/1317775805183717376?ref_src=twsrc%5Etfw">October 18, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
コミュ症大発揮．
TLが阿鼻叫喚で面白かった．（別に面白くはない）

### 開会式後から11月くらいまで
開会式の翌日から順次講義が始まるのだが，実はY-Ⅲは最初の週の講義が無かったのでこの間に更に開発を進めていた．
この1週間で構造体やドット・アロー演算子の実装に成功．
当初の目標ほどではなかったが，まぁまぁ進んだ状態で受講が始まった．

受講はオンラインなわけだが，原則的にRuiさんの[compiler book](https://www.sigbus.info/compilerbook)を見ながら進める感じで，授業みたいな講義はなく緩やかにやっていた．
一人ひとり画面を共有して進捗を報告したりプログラムを書いてるところを見せるのが主な流れで，疑問があればその都度質問していく．
これだけなのに合間合間で講師陣やチューターのhsjoihsさんからC言語の歴史とかこぼれ話が聞けてかなりためになるし，面白い．
多分こういう濃い話が聞けるのはここだけだと思う．

自分はマイルールで直接的な質問をしたり誰かのコードを丸写したりしないというルールを設けていたので，質問の代わりにじゃんじゃん進めてその部分を見てもらって意見をもらうという感じでやっていた．
見てもらって気づくのは，これで大丈夫やろーって実装したものが案外ハマりどころがあったりするというもの．
インクリメントとかも見せてみると，関数を対象にしたときとかでコケるとか自分で気づかない実装不足やバグが結構あった．
あと，構造体のAlignmentとか一人でやってたら知らなかった仕様とかも指摘してもらった．
これはもうY-Ⅲじゃないと難しい経験だったと思う．

実はsecampで初めて他人に見られながらコードを書く（オンラインでだけど）という経験をしたが，これはかなり緊張した．
いや，初めてにして見てもらう人が豪華過ぎたというのもあるが．
あとPCが非力すぎて苦しんだ．
いつもgccとvimとブラウザが動けばいいなーアハハくらいに考えている[^2]のだが，今回はオンラインでmeetを付けつつブラウザを立ち上げつつエディタを立ち上げながらテストをぶん回したりするので結構厳しかった．
まったく進まないテストをみんなで眺めたり...
今思い返せばブラウザが落ちたりそれ以前にWifiが1時間に1度落ちる不具合を抱えたまま参加してたな...（なんで直さないんですかね？）[^3]
みんなはまともなスペックのPCを用意しようね．

[^2]:このカスみたいな考えが後に悲劇を生む．
[^3]:フラグっていうのはこういうものを言う．

書く→見せる→フィードバックを繰り返しながら，じゃんじゃん開発を進めていった．
記録では，11月初週までに複合演算子とインクリメントのバグ[^4]を修正し，翌週に多次元配列を実装してる．

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">悲しいお知らせ <a href="https://t.co/yblVULbvXR">pic.twitter.com/yblVULbvXR</a></p>&mdash; and rsp,-0x10 (@\_Alignof) <a href="https://twitter.com/_Alignof/status/1326414953671168001?ref_src=twsrc%5Etfw">November 11, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">嬉しいお知らせ <a href="https://t.co/4HF4fCeAtC">pic.twitter.com/4HF4fCeAtC</a></p>&mdash; and rsp,-0x10 (@\_Alignof) <a href="https://twitter.com/_Alignof/status/1326467851394326533?ref_src=twsrc%5Etfw">November 11, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

ここらへんスタックの伸びる方向とかが段々分かんなくなっていて書いたり消したりしてたなぁ...
ずっとgdb-pedaとにらめっこしてた記憶．
あと，やっぱり配列とポインタの扱いの違いとかで延々仕様修正した気がする．
理解が難しいんだよなぁあそこ．

[^4]:たしか既存の演算子のノードを使った木に修正しようとしたら失敗した記憶

3週目は頑張ったみたいで，
- 構造体の中に配列が入れられるように
- メンバのalignmentを修正
- ラベルのシステムを変更してネストされた(if|for|while)文を可能に
- break文，continue文の実装
- 構造体の中に構造体や構造体のポインタを入れることが可能に
- 三項演算子の実装
- switch文の実装（途中）

をやったらしい．（ソースは週報）


