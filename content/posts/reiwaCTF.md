---
title: 令和CTF writeup
date: 2019-05-01T00:00:00+09:00
hideToc: false
description: 令和CTFのwriteup
enableToc: true
enableTocContent: false
author: Takana Norimasa
tags:
- CTF
- SECCON
categories:
- event
draft: false
---

> この記事は[令和CTF writeup - Qiita](https://qiita.com/Seigenkousya/items/2dc344c3bbe99b3b3d6c)から移転してきたものです．



知らなくて普通に一時間遅刻しました．
まぁ，早くいっても混んでたらしいですけど．
時間内にwelcome問題含めて2問，終わってから1問解けました．
バイナリにチャレンジして散りました．

## フラグの例は？
いわゆるサービス問題です．問題文からコピペ．

```
SECCON{reiwa}
```
これがあるのと無いのでは精神的にも違う気がする．
## bREInWAck
名前からしてbrainf*ckな気がします．
brainf*ckの命令を平成令和「」．に置き換えたものなんだろうなと予想．

```
令和和和和和和和和和和和和和和和和「令和
和和和和令和和和和令和和和和和和和令和和
和和和和令和和平平平平平成」令和和和。令
和和和和和。成成。。平成成成成。成。令令
和和和和和和和和和和和。令和和。平平平和
和和和。令和和。和和和和。令令和和和和和
和和和和和和和。平平平和和和和和和和和和
和和和和。成成成成成成成成。令成成成成成
成成成。令令。成成成成成。成成成成成成。
令和。平平和和。令令令和和和和和和和和和
和。
```

wikipediaによるとbrainf*ckの命令は以下の八つだそうです．

>  \> ポインタをインクリメントする．ポインタをptrとすると，C言語の「ptr++;」に相当する．
   < ポインタをデクリメントする．C言語の「ptr--;」に相当．
   + ポインタが指す値をインクリメントする．C言語の「(*ptr)++;」に相当．
   - ポインタが指す値をデクリメントする．C言語の「(*ptr)--;」に相当．
   . ポインタが指す値を出力に書き出す．C言語の「putchar(*ptr);」に相当．
   , 入力から1バイト読み込んで，ポインタが指す先に代入する．C言語の「*ptr=getchar();」に相当．
   [ ポインタが指す値が0なら，対応する ] の直後にジャンプする．C言語の「while(*ptr){」に相当．
   ] ポインタが指す値が0でないなら，対応する [ （の直後[1]）にジャンプする．C言語の「}」に相当[2]
[Brainfuck - Wikipedia](https://ja.wikipedia.org/wiki/Brainfuck)

うーん．言いたいことは分かるけど...
命令が7つしか問題に出てこないのでパターンから置換して実行した方が早いなということで適当なサンプルを見つけてきます．
[わかりやすくbrainf*ckについて解説している記事](https://qiita.com/TomoShiozawa/items/25dcce1540085df71053)があったのでそこのhello worldを参考にしました．
>
```:hello_world.bf
+++++++++[>++++++++>+++++++++++>+++>+<<<<-]>.>++.+++++++..+++.
>+++++.<<+++++++++++++++.>.+++.------.--------.>+.>+.
```
[Brainfuck 超入門 - Qiita](https://qiita.com/TomoShiozawa/items/25dcce1540085df71053)

+ばっかりじゃないか(驚愕)．これは和とかけているに違いない(確信)．
もっと言えば，[]は「」に対応しているんじゃないかと．繰り返しの部分とぴったりです．
どうやら，総当たりはいらなそうで一安心．
「のあとに来ているので>は令ではないかと予測．
こんな感じで，以下の対応表ができた．

|before|after|
|:-:|:-:|
|令|>|
|和|+|
|平|<|
|成|-|
|。|.|
|「|[|
|」|]|

置換したらこんな感じ．

```
>++++++++++++++++[>+
++++>++++>+++++++>++
++++>++<<<<<-]>+++.>
+++++.--..<----.-.>>
+++++++++++.>++.<<<+
+++.>++.++++.>>+++++
+++++++.<<<+++++++++
++++.--------.>-----
---.>>.-----.------.
>+.<<++.>>>+++++++++
+.
```
あとは動かすだけ．
以下のサイトが途中経過がみられて勉強になるのでおすすめ．
[Brainfuck Visualizer](https://fatiherikli.github.io/brainfuck-visualizer/)

```
SECCON{bREIn_WAnic!}
```
素早くとけてスッキリ．
## 新元号発表
みんな大好きQRコード．まぁ地道に解けばいけるだろ，と思っていましたが全然解けず翌日の夕方にやっと解けました．まさかこんなオチなんて...盲点．
newera.pdfが渡されて，開くとこんな感じ．
![img_03.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/318539/f177d6af-960c-dafa-eb0f-b143a24b204e.png)
とりあえず，みんなの恋人foremostをつかって調べてみる．

```
# foremost newera.pdf
File: newera.pdf
Start: Wed May  1 00:18:51 2019
Length: 77 KB (79665 bytes)
 
Num	 Name (bs=512)	       Size	 File Offset	 Comment 

0:	00000019.jpg 	      41 KB 	       9827 	 
1:	00000102.jpg 	      12 KB 	      52646 	 
2:	00000000.pdf 	      77 KB 	          0 	 
Finish: Wed May  1 00:18:51 2019
```
やっぱり，前の画像とQRのある後ろの画像は別々．
出てきた画像からとったQRがこれ．
![000000019.jpg](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/a6c9e9da-bded-f80c-f9d8-4d7baed0fb6e.jpeg)
QR問題の味方，[https://github.com/waidotto/strong-qr-decoder/](https://github.com/waidotto/strong-qr-decoder/)でとりあえずやってみることにする．
またあの地味な手打ちをするのか...と観念しながら頑張ってみるも出ない．
かなり頑張ったが出ない．それでも粘るが出ない．
![Screenshot from 2019-05-01 13-04-55.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/28ad6565-c58b-a080-c07f-d33aa3b0450d.png)
画像と重ねたりして確かめてみても出ない．
観念してlibreoffceをインストールして見てみると，意外と楽に画像が動かせる．あれ？
![Screenshot from 2019-05-01 20-38-07.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/93606df8-f04a-8cd9-c352-29f2aeb6af72.png)
出たわね．これまでの頑張りを返して(切実)
GIMPで黒い部分を抽出して合成して，
![qr_data.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/11146044-9ab2-71b5-a323-08c56d335179.png)
合成が下手なのでツールで手打ちして読み込んで完成．

```
The flag is SECCON{overlay_overlap_overera}
```

## 反省
バイナリに手が出なかったので反省．
何か毎回バイナリでつまるので特訓したい的なことをいってる気がする．
web系もサーバ系もダメなのでこれから頑張る．


## 参考
[Brainfuck 超入門 - Qiita](https://qiita.com/TomoShiozawa/items/25dcce1540085df71053)
[Brainfuck Visualizer](https://fatiherikli.github.io/brainfuck-visualizer/)
[GitHub - waidotto/strong-qr-decoder: 強力なQRコードデコーダ](https://github.com/waidotto/strong-qr-decoder/)


