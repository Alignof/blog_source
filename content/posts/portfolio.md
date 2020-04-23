---
title: "ポートフォリオサイトを作った"
date: 2020-04-23T01:29:18+09:00
description: ポートフォリオの建設がようやく終了したのでメモ。
hideToc: false
enableToc: true
enableTocContent: false
author: Takana Norimasa
authorEmoji: false

tags:
- 技術活動
- html
- js
- css
- web
categories:
- tech
draft: true
---

## お知らせ
このブログができるずっと前から建設を進めていたポートフォリオがようやく完成しました。
疲れた...（満身創痍）
上のバーのAbout meからいつでも見られます。
link:[https://takana-norimasa.github.io/](https://takana-norimasa.github.io/)
レポジトリを見てみると去年の10/22から始まってますね（実際はそれよりちょっと前だけど）

## 経緯
実はこのブログを作る前からずっと作りたかったものの一つで、Webの知識が少しでも欲しくて入門編にしたかったのと他の人のポートフォリオを見ていいなぁと思ったからというのが主な動機です。
今までにも何度か触ったことがあるのですがとても実用的なものではないですし...（高専プロコンの競技用のシュミレータ作ったりとかで触ったけど）
自分の作ったものをまとめたら良い自己紹介がわりになるし、バラバラになっている成果も集約できるかもと思いながら作業に入りました。
実際はかなり大変だった...

## 振り返り
それじゃあ振り返っていきましょう。
レポジトリはこちら。（実装がひどすぎるので見せたくないけど）
<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0;"><a href="https://github.com/Takana-Norimasa/Takana-Norimasa.github.io" data-iframely-url="//cdn.iframe.ly/api/iframe?url=https%3A%2F%2Fgithub.com%2FTakana-Norimasa%2FTakana-Norimasa.github.io&amp;key=dd60c159c87f40f1ecca839b51b281e8"></a></div></div><script async src="//cdn.iframe.ly/embed.js" charset="utf-8"></script>

### 構想段階
僕はWebの知識は皆無なのでライブラリでゴリ押すか逆にそれらに頼らず力押しするかのどっちかだったのですが、ちょうど思いついたアイデアがライブラリなしで行けそうだったので力押し作戦をとることにしました。
思いついたアイデアはターミナルの再現。インタラクティブにターミナル操作の要領で説明が出てくる感じです。
これならオシャレなセンスも要らないし見ていて楽しいかなぁと思ったのでこれにしました。

### 初期段階
とりあえず最初に思いついたギミックがタイピングアニメーションだったのでそれからやり始めることにしました。
流石にこれを実装するのは骨なのでライブラリみたいなの無いかなと探してここで結構な時間かけて実験して選定しました。
なんどもここで全消しした記憶。
結局[t.js](https://github.com/mntn-dev/t.js?files=1)を採用しました。
理由としてターミナルの操作次第で出力が変わるので細かい指定を埋め込むhtml側に入れたいというのと書いて消すというアニメーションがあったのが大きいです。

### 中盤
見た目を整えたりボタンを実装したり...
この時点でクリックした操作に応じてコマンド操作のアニメーションが出るって感じの方針が固まりました。
ちなみにターミナルの見た目は僕が普段使っている設定そのものです。
最初に出てくるAAもここで作りました。
フォントによって表示がめちゃくちゃになる（形が崩れたりバックスラッシュと円マークがめちゃくちゃだったり...）のでWebフォントで整えることを覚えました。
他にもgithubやtwitterのアイコンをリンクの前に付けてみたり選択するボタンごとに実行するコマンドを割り当てたりもしてました。

この時点で結構いい感じにターミナルっぽくなってました。
最初は無理だと思っていた階層構造も上手くボタンの選択肢を絞れば簡単に実現できましたし、それぞれの機能の関数化もだいたい済んでました。（本当に関数を組み合わせるだけ）
ここらへんから地獄の入り口、同期処理が入ってきます。
かなり勉強になりました。（n敗）
async/awaitについて勉強して任意のタイミングでタイピングアニメーションを実行することができました。
```js
async function main_stream(){
	await typing(wait);
	await typing(hello);
	await message(welcome_message);
	await typing(cmd("whoami"));
	await message(about);
	await typing(cmd("ls -a"));
	await message(ls_root);
}
```
こんな感じで上手いこと同期をとっていかないとターミナルみたいに動いてくれません。
一気に表示されちゃったりまだ前のが上手く表示されてない内に次に行っちゃったり大変でした。
タイピングアニメーションやhtmlのjsでの埋め込みのタイミングをとるのが難しかったです。
ただ、完全な同期処理にならずawaitとdelayを使った簡易的なものでした。

### 終盤
一番辛くてダレた「文字を書く」という作業です。
つまり、ポートフォリオの内容の部分ですね。
ここが一番時間がかかったしモチベーションが低かったところだと思います。（リアルで他にやることがあったし）
本気出せば2日くらいで終わる作業だったな...（今思えば）
テストページにhtmlで記事を書いて最後にjsの変数として編集するって感じですね...（地獄）
あとは見栄えが良くなるように[Iframely](https://iframely.com/)を使ってみたり工夫してみまたりcssを微調整してました。（最初のgithubのリポジトリへのリンクはIframelyを使ってます）

### 末期
仕上げにして地獄です。
とりあえず、どんどん下に表示が足されているのにスクロールがそのままで見えなくなっていくのが気持ち悪かったので下部にダミーのタグを用意してそれを追いかける感じでスクロールさせました。
```js
function scroll_bottom(){
	const targetElement=document.getElementById('blank');
	const rectTop=targetElement.getBoundingClientRect().top
	const offsetTop=window.pageYOffset
	const buffer=50
	const top=rectTop + offsetTop - buffer
	window.scrollTo({top,behavior: "smooth"});
}
```
```<body>```の最後に```<div id="blank">```というタグがあるイメージ。
個人的に気に入っている処理。

最大の問題だったのが同期処理です。
軽い処理だからdelayの時間を決め打ちしてasync/awaitとdelayを併用すれば行けるでしょ。とか思っていたらやっぱりダメでした...（当然）
でもt.jsはjQueryなのでcallbackを基準に使うしか無いし...（ここで浮き彫りになる技術力不足）
他はasync/awaitで動いているのでそっちに合わせるのも不可能だしawaitを使っても同期されるのは呼び出されるタイミングだけでhtmlを挿入して実際に動き終わるタイミングはt.jsが用意したcallbackのみぞ知るって感じなんですよね...
肝心のアニメーションの終わりがわからないと次の出力とかコマンド操作とかに進めないし...
結局所定のcallback関数で元のasync funcのresolve()を呼び出すという世紀末的な解決をして今回はひとまず終了ということにしました。（一応理想通りに動いたので）

```js
const tjs=function(num,resolve){
	//t.js
	$((".terminal_"+num)).t({
		/* some config and process*/

		// finished callback
		fin:function(elm){
			$('terminal_'+num).find('.t-caret').css({opacity:0});
			counter++;
			resolve();// <- quit async function (and typing func)
		}       
	})
}

function typing(text){
	const p=new Promise(async(resolve,reject) => {
		scroll_bottom();
		await new Promise(r=>setTimeout(r, 100));
		time_update();
		terget.insertAdjacentHTML('beforeend',text);
		tjs(counter,resolve);
	});
	return p;
}
```
tjsという関数の先にt.jsのjQueryが待ち受けているって感じです。
そこの終了時のcallbackで渡されたresolveを実行しています。

## 反省
まぁ自分が実現したい機能をすべて達成できたのは良かったです。
あんまりHTMLとかCSSとかJSって触ったことなかったのでいい勉強になりました。
それでも反省すべき点は色々あって、

- スマホとかだと操作しづらい（いわゆる非レスポンシブデザイン）
- 結局jQueryが何者なのか完全なる理解が得られなかった
- 最新技術とは程遠い気合のWebページなのでそれらの勉強はできなかった
- 同期処理が完全な形ではない（だがこれを上回る方法があるのかは一切不明）
- 保守性の著しい欠如（いちいちhtmlに戻してjsの変数に変換するのは厳しい）
- ギミック不足（もう少し機能がほしい）
- 初めての人には分かりづらいかも（別でこのサイトに作るか？）
- そもそも書くほどの成果がない（それはそう）

あたりは大きな反省点です。
これらはまた、勉強したらおいおい直していきたいです。
恥を晒すのも勉強の一つということで。

これを作ったらTLに無限に流れてくる難解なWeb用語も分かるかな？とか思ってましたが、構想段階でモダンなあれこれの採用を見送ってしまったので次はVue.jsを使ってみたいです。（なんなのかよく分かってない人）
オシャレなサイトも作ってみたいなぁ。

## 次は何やる？
次はSecHackの成果発表会に向けての準備と去年からやりたかったCコンパイラの自作に踏み切ろうと思います。
SecHackでやってる人を見てずっとやりたかったんですよね。自作コンパイラ。
まぁそれも記事にしたり今回作ったポートフォリオに入れていきたいですね。

