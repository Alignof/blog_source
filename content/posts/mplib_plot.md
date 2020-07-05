---
title: matplotlibで特定のデータをプロットしない方法
date: 2019-02-26T18:44:25+09:00
description: matplotlibで特定の項目にだけマーカーをつける方法
hideToc: false
enableToc: true
enableTocContent: false
author: Takana Norimasa
tags:
- Python
- matplotlib
categories:
- tech
draft: false
---

> この記事は[matplotlibで特定のデータをプロットしない方法 - Qiita](https://qiita.com/Seigenkousya/items/2200bc4448a861b826e5)から移転してきたものです．

## はじめに
[漫画の掲載順を取得してグラフ化する記事](https://qiita.com/Seigenkousya/items/8f0ffbd2c34a8e8535e2)を書いている時に休載で掲載順を取得できない月があり，グラフ化するときに困った．
matplotlibで特定のデータをプロットしない方法が後から分かったのでメモ．

## 環境
```
# uname -a                                                                                                                              
Linux kali 4.18.0-kali2-amd64 #1 SMP Debian 4.18.10-2kali1 (2018-10-09) x86_64 GNU/Linux
# python --version                                                                                                                             
Python 3.7.2+
# pip3 show matplotlib                                                                                                                         
Name: matplotlib
Version: 2.2.2
```
## 問題
例えば，以下のようなデータがあったとする．

|month|1月|2月|3月|4月|5月|6月|7月|8月|9月|10月|11月|12月|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|data|13|15|21|5|10|　|21|17|15|16|21|13|

6月だけデータがない．

```python
Y_data=[13,15,21,5,10, ,21,17,15,16,21,13]
```

Y軸のデータの配列に空きができてしまった．どうすればいいのか．

## 解決法

プロットしたくないor欠損しているデータにはNoneを代入するとその項目はプロットされなくなる．


```python
Y_data=[13,15,21,5,10,None,21,17,15,16,21,13]
```
こんな感じ．

```python
#!/usr/bin/env python 
import matplotlib.pyplot as plt
 
X_data=[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
Y_data=[13,15,21,5,10,None,21,17,15,16,21,13]
month_name=['Jan.','Feb.','Mar.','Apr.','May','Jun.','Jul.','Aug.','Sep.','Oct.','Nov.','Dec.']

plt.xlabel('month')
plt.ylabel('data')

plt.xticks(X_data,month_name)
plt.plot(X_data,Y_data)
plt.show()

```
>結果
![plot_None.png](https://qiita-image-store.s3.amazonaws.com/0/332794/0a8a2996-b039-6287-047d-732a0df39434.png)

一件落着．
## 参考文献
[python - matplotlibにおけるグラフの始点の指定 - スタック・オーバーフロー](https://ja.stackoverflow.com/questions/41200/matplotlib%E3%81%AB%E3%81%8A%E3%81%91%E3%82%8B%E3%82%B0%E3%83%A9%E3%83%95%E3%81%AE%E5%A7%8B%E7%82%B9%E3%81%AE%E6%8C%87%E5%AE%9A)
これのお陰で助かりました．ありがとうございます．

