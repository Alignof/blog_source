---
title: "セキュリティ・キャンプ全国大会2020に参加してきた<1>"
date: 2020-12-31T01:31:30+09:00
description: seccamp 全国大会2020の参加録（前編）
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

### 開会式後から11月中旬くらいまで
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

### 11月第3週
3週目は頑張ったみたいで，
- 構造体の中に配列が入れられるように
- メンバのalignmentを修正
- ラベルのシステムを変更してネストされた(if|for|while)文を可能に
- break文，continue文の実装
- 構造体の中に構造体や構造体のポインタを入れることが可能に
- 三項演算子の実装
- switch文の実装（途中）

をやったらしい．（ソースは週報）

メンバのalignmentとか本当に初めて知った．
structって上手いことサイズが最小になるように詰め直しとかするのかなと思ったけど，そうじゃないのは意外だった．
ここらへんでようやくスタックに対するサイズ確保の計算が完璧になった感じ．

もう1つ辛かったのがアセンブリのラベルでこれを管理するのが結構キツい．
if, for, whileあたりまでは良かったのだが，これにbreak, continueとかが入ると途端にバグって大変だった．
特に入れ子になってるとこれはどこのラベルと対になってるんだ...という気持ちに無限回なった．（これが地味に最大の敵だったかもれない）

### 11月第4週
4週目はなんと驚き講義最終日で（エーーーッ）ゼミの最終発表があった．
早い...早くない？
未だにセルフホストを諦めていなかった自分は必死にセルフホストに必要な機能を実装し続ける．
この週は，
- switch文
- do-while文
- 列挙型
- スコープ
- void
- typedef

を実装したらしい．（今見たらすごい実装量だ...）
switch文は先週までにあらかた実装が終わっていたのだが，@hsjoihs氏にDuff's deviceってコードを教えてもらってひっくり返った記憶．

```C
int main(){
	char *psz1 = calloc(100, sizeof(char));
	char *psz2 = "abcdefghijklmnopqrstuvwxyz";
	char *to   = psz1;
	char *from = psz2;
	int  count = 26;

	switch (count % 8) {
		case 0:  do {  *to++ = *from++;
		case 7:        *to++ = *from++;
		case 6:        *to++ = *from++;
		case 5:        *to++ = *from++;
		case 4:        *to++ = *from++;
		case 3:        *to++ = *from++;
		case 2:        *to++ = *from++;
		case 1:        *to++ = *from++;
			} while ((count -= 8) > 0);
	}

	printf("to	:%s\n", psz1);
	printf("from	:%s\n", psz2);
}
```

switch文なんてif-elseの変形みたいなもんだし余裕やろｗとか思ってた（ナメプ）のでそんな〜〜〜の気持ちになった．
C言語黒魔術ポイントがかなり高いコードだと思う．
これが正しく動くようにするのはかなり大変で，ラベルの概念の導入とか意外とやることが多かった...
でもこれが動いたときかなり自信がついたし，Cコンパイラを自分の思うままに書いてるんだという感覚が湧いてきて嬉しかった．

他にもdo-whileやenum，スコープをやった．
変数を連結リストで管理していたのでスコープの実装はポインタを張り替えるだけでスッと書けて良かった．
ここまで考えてあるあたりもcompilerbook最高ポイントだと思う．

typedefはかなりの曲者でこれを実装してしまうと型のテーブルを持つ必要があり，パーズもかなり面倒になって大変だった．
一気にコンパイラ全体の難易度が上がる気がする．
セルフホストには必要ないので急いでるなら実装しないほうが良いかもしれない．
これもキツかったなぁ...型のスコープとかも存在してデータ構造が増えるし，地味にパターンが多いし...
でも，セルフホストするときのコードの見栄えはかなり良くなるし，学びも多いのでセルフホストしてから戻ってきて実装するのはアリかも．

ここまでかなりの実装を重ねセルフホストできるくらいの機能を獲得したものの，セルフホスト自体には手が回らずあえなくゼミ内の最終発表に．
来週には全体発表があるのでゼミの発表者に志願しておいた．
この時点で僕と同じくらい進んでいたあざらしくん([@azarashi\_uni](https://twitter.com/azarashi_uni))に資料作成などの補佐をお願いした．
僕は始まる前から開発していたのにこの時点で並びかけていたので，彼の実装スピードは凄まじいものだと思う．

### 〜最終発表
最終発表までにどうにかセルフホストをしたいというお気持ちで準備を始める．
まず，セルフホストを簡単にテストするために環境を整える必要があった．
これがまぁまぁ大変．Makefileをガチャガチャしてる間に結構時間を持ってかれた記憶がある．

環境が構築できたら取り敢えず自作Cコンパイラに自分のソースコードを喰わせてみる．
当然落ちる．（そんな...）
というか初っ端のtokenizeで落ちてる模様．
ここから地獄のデバッグタイムが始まる．

そして同時に資料作成も始まる．
自分のゼミでの最終発表の資料をベースにだらだら書いてた．
というか最終稿は発表前日の夜中から書き始めたし，なんなら発表10分前でも書きまくってた気がする．
なんだかんだギリギリまでセルフホストと戦っていた僕とあざらしくんだが，とうとうどちらもセルフホストにたどり着くこと無く最終発表まで来た．
セルフホストの道のりは険しい．

結局，コードの一部を自分のソースコードに置き換えることで完動するフランケン・コンパイルは動いていたのでそこまでの内容で発表することにした．
しかし，ここで（かなりの）問題が起こった．[^5]
ここまで散々悲鳴を上げていてゼミのみんなからも心配されていた僕のPCくんが発表するために画面を奪った瞬間死亡したのだ．
...さもここからどうにかなったようなプチハプニングのように書いているが，この男あろうことかそのことに気づかない．
資料を向こうで出してもらってることを信じて必死に発表を始める．
手元のスマホで資料を見ながら必死に虚空に向けてしゃべること約5分．PCの時計が全く進んでないことに気づいた．
あっ終わった．

[^5]:そう，かなりの．

思えば自分はトラブル王として有名だった．
ハッカソンに出かければ必ずマシンが止まり，ハンズオンに出れば必ず環境構築に失敗する．
自分だけデータが飛んだり何故かWifiがつながらなかったりイベントの前日にOSが消し飛んだり...エトセトラエトセトラエトセトラ．
それが最悪の形で出てしまった．オタク反省．

ちなみにこれを見越して配属されていたあざらしくんが僕の資料を使ってどうにか発表してくれたらしい．

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">Cコンパイラゼミの発表は冗長化されており、呼び系である替え玉発表（公式）が実行されたのでなんとかサービスを維持できた。<a href="https://twitter.com/hashtag/seccamp?src=hash&amp;ref_src=twsrc%5Etfw">#seccamp</a></p>&mdash; hikalium (@hikalium) <a href="https://twitter.com/hikalium/status/1335424813603557379?ref_src=twsrc%5Etfw">December 6, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

マジで申し訳ない...
これを読んでいる良い子のお友達は，普段から徳とPCのスペックを積んでおくようにしようね．

とにかく色々あったが，これで僕が参加したseccamp2020は一区切りついた．
が，まだセルフホストという野望が潰えたわけではない...
大会が終わってもモチベーションは高いままだった．

## ダラダラ書きすぎ
ここからセルフホストまでアツいバトルが始まるのだが，流石にダラダラ書きすぎたし長くなったので後編に分けようと思う．
だってこの記事を書き始めたのが2020年の大晦日で，久しぶりにファイルを開いてみた今日が2021年の12/01である．
約1年以上放置してたことになる．[^6]

[^6]:そんな...

流石にこれ以上はアレなのでここまでを前編としてこのあとを後編とすることにした．
後編ではセルフホストまでの道筋だけじゃなくてデバッグの勘所とか検証環境の構築の話とかを書く予定なので乞うご期待．



