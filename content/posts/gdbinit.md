---
title: "gdbinitを使い分ける"
date: 2020-04-28T13:41:17+09:00
description: gdb dashboardとgdb-pedaを使い分けるための奮闘録
hideToc: false
enableToc: true
enableTocContent: false
author: Takana Norimasa

tags:
- gdb
- gdb-peda
- memo
categories:
- tech
draft: true
---

## 経緯
結構詰まったのでメモ。
今まで普通のCのデバッグにはGDB、アセンブラを読むときには拡張のgdb-pedaを使っていた。
つまりgdbを使うときは、
```shell
$ gdb -nx terget_file
```
gdb-pedaを使うときは、
```shell
$ gdb terget_file
```
としていたのだ。

最近になって本格的にCのデバッグをするようになった（それまではpedaしか使ってなかった）のでgdb dashboardを導入することにした。
しかし、gdb dashboardもgdb-pedaも~/.gdbinitを使って機能の拡張を行うのでどちらか一方しか拡張機能を使えない。
Cとアセンブラによって拡張機能を使い分けたいのでこれは困った...

## ~/.gdbinitの使い分け
2つの拡張機能を利用するにはどうにか上手いこと2つのgdbinitを使い分けるのが理想的だ。
いい感じにgdbinitの参照先を指定できるオプションがあれば良いのだが...

### 解決方法
かなりの試行錯誤の末ついに方法を見つけた。
まず、拡張機能ごとにgdbinitを分ける。
自分の場合はgdb dashboardは~/.gdbinitに、gdb-pedaは~/.gdbinit_pedaにそれぞれ設定を書いた。
これで普通にgdbを実行したときには~/.gdbinitが読まれるのでgdb dashboardが使える。
では、gdb-pedaを使いたい場合はどうするのか？
gdb-pedaを使うときは以下のようにコマンドを叩く。
```shell
gdb -nx -ix=~/.gdbinit_peda terget_file
```
-nxでデフォルトの~/.gdbinitを読まないようにして-ixで新しい~/.gdbinit_pedaを読ませるようにしている。
```gdb --help```の
> --init-command=FILE, -ix
Like -x but execute commands before loading inferior.

の部分が設定ファイルの項目だと気づくのに時間がかかった。
後はzshrcに以下のようにaliasの設定をすれば
```zsh
alias gdb-peda='gdb -nx -ix=~/.gdbinit_peda'
```
2つの拡張機能をコマンド1つで使い分けることができるようになる。
```shell
# gdb dashboard
$ gdb 

# gdb-peda
$ gdb-peda 
```

これで一見落着。

