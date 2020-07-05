---
title: matplotlibで特定のデータにだけマーカーを適用する方法
date: 2020-03-14T18:44:25+09:00
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

> この記事は[matplotlibで特定のデータにだけマーカーを適用する方法 - Qiita](https://qiita.com/Seigenkousya/items/1a4691a2067c71e1b5f2)から移転してきたものです．

## はじめに
[雑誌の掲載順をグラフ化するとき](https://seigenkousya.github.io/post/kirara_order_2020/)に，matplotlibで特定の項目にだけマーカー（グラフに打つ点）をつけたくなった（センターカラーのときにだけわかりやすいように目印をつけたかった）が，探しても全く出てこなかったのでメモ．
![max_2020.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/137da981-190f-4ff5-291f-3301a27bb9f7.png)
↑こんな感じで強調するために特定の値の時だけマーカーを適用したかった．

## 環境
```
$ uname -a                                                                                                                              
Linux kali 4.18.0-kali2-amd64 #1 SMP Debian 4.18.10-2kali1 (2018-10-09) x86_64 GNU/Linux

$ python3 --version                                                                                                                             
Python 3.7.6

$ pip3 show matplotlib                                                                                                                         
Name: matplotlib
Version: 3.1.2
```
## 問題
例えば，以下のようなデータがあったとする．

|month|1月|2月|3月|4月|5月|6月|7月|8月|9月|10月|11月|12月|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|data|13|15|21|5|10|18|21|17|15|16|21|13|

これらをグラフにするとこうなる．
![before.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/3312de61-b11e-27af-75ec-ecc7a347cdfe.png)

このグラフの1,4,7,10月のデータにだけダイヤモンドでマーカーを付けたい（その他には付けたくない）ときどうすればいいだろうか．

## 解決法
マーカーを付けたい部分だけを配列にしてプロットするときに```markevery=```で渡す．
X番目にマーカーを付けたければX-1番目の数を配列に追加する．


こんな感じ．

```python
#!/usr/bin/env python 
import matplotlib.pyplot as plt
 
X_data=[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
Y_data=[13,15,21,5,10,18,21,17,15,16,21,13]
month_name=['Jan.','Feb.','Mar.','Apr.','May','Jun.','Jul.','Aug.','Sep.','Oct.','Nov.','Dec.']
mark_point=[0,3,6,9]

plt.xlabel('month')
plt.ylabel('data')

plt.grid(color='gray')
plt.xticks(X_data,month_name)
plt.yticks(range(1,max(Y_data)+1))
plt.plot(X_data,Y_data, '.', linestyle='solid', marker="D", markevery=mark_point)
plt.show()
```
> 結果
![markeevery1.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/f510793f-c282-a5d7-9e63-aa595a089571.png)

y軸のデータを基準にしたければ，先にデータを比較して配列に格納すれば良い．
例）データが奇数のときだけマーカーを適応する．

```python
#!/usr/bin/env python 
import matplotlib.pyplot as plt
 
X_data=[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
Y_data=[13,15,21,5,10,18,21,17,15,16,21,13]
month_name=['Jan.','Feb.','Mar.','Apr.','May','Jun.','Jul.','Aug.','Sep.','Oct.','Nov.','Dec.']
mark_point=[]

for i,data in enumerate(Y_data):
    if data%2:
        mark_point.append(i)

plt.xlabel('month')
plt.ylabel('data')

plt.grid(color='gray')
plt.xticks(X_data,month_name)
plt.yticks(range(1,max(Y_data)+1))
plt.plot(X_data,Y_data, '.', linestyle='solid', marker="D", markevery=mark_point)
plt.show()
```
> 結果
![markeevery2.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/f45b37cb-eec5-96c4-6b4d-89a766d9a769.png)

一件落着．
## 参考文献
[Markevery Demo — Matplotlib 3.1.2 documentation](https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/markevery_demo.html)


