---
title: SECCON Online 2019 Quals Writeup
date: 2019-10-22T00:00:00+09:00
description: SECCON Online 2019 QualsのWriteup
hideToc: false
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

> この記事は[SECCON Online 2019 Quals Writeup - Qiita](https://qiita.com/Seigenkousya/items/09cfe476a775f41d24e3)から移転してきたものです．


###  はじめに
予定が合わず友達からポケットWifiを借りて出先から参戦．
サービス問題除いて一問しか解けませんでした（絶望
何か去年より難しいと思ったのは僕だけですかね...?
一応，闘いの記録ということで...

###  Writeup
### Welcome
いつものIRCトピックを見る奴．
毎回どうするか一瞬焦る．

```
SECCON{Welcome to the SECCON 2019 Online CTF}
```

### coffee_break
唯一まともに解けた問題．
以下のpythonファイルと暗号化された文字列があるから復号してね！
ってやつ．

```python:enctypt.py
import sys
from Crypto.Cipher import AES
import base64


def encrypt(key, text):
    s = ''
    for i in range(len(text)):
        s += chr((((ord(text[i]) - 0x20) + (ord(key[i % len(key)]) - 0x20)) % (0x7e - 0x20 + 1)) + 0x20)
    return s

key1 = "SECCON"
key2 = "seccon2019"
text = sys.argv[1]

enc1 = encrypt(key1, text)
cipher = AES.new(key2 + chr(0x00) * (16 - (len(key2) % 16)), AES.MODE_ECB)
p = 16 - (len(enc1) % 16)
enc2 = cipher.encrypt(enc1 + chr(p) * p)
print(base64.b64encode(enc2).decode('ascii'))
```

暗号化された文．

```
FyRyZNBO2MG6ncd3hEkC/yeYKUseI/CxYoZiIeV2fe/Jmtwx+WbWmU1gtMX9m905
```

フラグをこのpythonスクリプトで暗号化すると以上のような文字列になるらしい．
ならば逆に辿っていけばもとのflagにたどり着けるはず．
encrypt.pyの大まかな流れを整理してみる．

1.　key1とtext（これが平文かつflag）をencrypt()関数に与えてenc1を得る．
2.　key2からcipherをenc1からpを求める．
3.　cipher.encrypt()にenc1とpを与えてenc2を得る
4.　enc2をbase64でエンコードしてさらにそれをASCIIでデコードする
5.　4を出力

これを5から1に向かって辿って最終的にtextの値が何なのか分かればflagが分かる．

とりあえず，任意の文字列をencrypt.pyで暗号化して，暗号化した途中の値と復号化スクリプトの途中の値を突き合わせて解いた．
これなら少しずつあってるか確認しながら解ける．

### #Step1
復号するときは暗号化する手順の逆から見ればいいので，最後の出力部であるprintから見る．

```python
print(base64.b64encode(enc2).decode('ascii'))
```
出力された暗号文＝enc2をbase64でエンコードしたものをASCIIでデコードしたもの
ということは，逆にすると，
enc2=出力された暗号文をASCIIでエンコードしたものをbase64でデコードしたものとなる．

コードにするとこんな感じ．

```python
rev1=base64.b64decode(out.encode('ascii'))
```
Step1の結果がrev1に入っている．
これは，encrypt.pyのenc2とまったく同じになる．

### #Step2
enc2まで遡れたので，次はenc1まで遡る．
enc2を求める処理は，

```python
key2 = "seccon2019"

cipher = AES.new(key2 + chr(0x00) * (16 - (len(key2) % 16)), AES.MODE_ECB)
p = 16 - (len(enc1) % 16)
enc2 = cipher.encrypt(enc1 + chr(p) * p)
```
となってる．これを逆算してenc1を求めればよい．

まず，cipher.encrypt()に関してだが，運良くdecrypt()も存在する．つまり，ここの部分に関してはそのままdectypt()に置き換えればよさそう．
つぎに括弧の中身である```enc1 + chr(p) * p```だが，decrypt()した後ものから```chr(p) * p```を引けばよさそうだ．

しかし，もう一度よく見てほしい．
pythonにおいてchr()*nの計算は数値計算ではない．
実際にencrypt.pyのrev1の値をcipher.decrypt()した値を見ればよく分かるが，

```python
b"'jff~|Ox9'34G9#g52F?489>B%|)173~)%8.'jff~|Q\x05\x05\x05\x05\x05"
```
末尾に不自然な\x05が複数くっついている．これこそが```+ chr(p) * p```の正体なのだ．
つまり，```+ chr(p) * p```は数値を足していたのでは無く，chr(p)　(今回なら\x05)という文字列をp回enc1にくっつけていたのである．

これより，

```python
rev2=cipher.decrypt(rev1)
rev3=rev2.decode('ascii').replace("\x05","")
```
rev2の行でcipher.decrypt()で復号化を行い，
rev3の行で末尾の適当な文字列を取り除いてASCIIに復号することでenc1が求まる．
chr(p)の値（replace()の中身）はrev2の中身から予測すればよい．
rev3とencrypt.pyのenc1はまったく同じものになる．

### #Step3
enc1が分かったのでそこから平文を逆算する．
enc1を求める処理は以下の部分．

```python
def encrypt(key, text):
    s = ''
    for i in range(len(text)):
        s += chr((((ord(text[i]) - 0x20) + (ord(key[i % len(key)]) - 0x20)) % (0x7e - 0x20 + 1)) + 0x20)
    return s

key1 = "SECCON"
enc1 = encrypt(key1, text)
```
encryptの引数であるtextが平文(=flag)である．ゴールは近い．
decryptというencrypt()とは逆の動きをする関数を作ればよい．

encrypt()の動きは大まかに言って平文の各文字に以下の処理をしているだけである．

```python
s += chr((((ord(text[i]) - 0x20) + (ord(key[i % len(key)]) - 0x20)) % (0x7e - 0x20 + 1)) + 0x20)
```
これの逆算には随分骨が折れそうだ．
とりあえず，処理を細分化して順番に並べてみる．

1. textのi番目の文字列をord()して数値に戻したものに0x20を足す．
2. key1の {iを1keyの長さで割った余り} 番目の文字をord()で数値に戻したものに0x20を引く．
3. 1と2を足す．
4. 3を(0x7e - 0x20 + 1)で割ったあまりを出す．
5. 4に0X20を足す．
6. これをchr()でASCIIに変換

これを逆からやればいい．
曲者は4だ．余剰を使ってるので値を一意に定められない．幸い，flagの最初は```SECCON{```なのでそれを手がかりに総当たりすればいい．

1. ord()で文字を数値に変換．
2. 1から0x20を引く．
3. xをyで割った余りmからxを求めるには，m*n(nは任意の数字)をしてxに該当するnを求めればよい．今回は最初の文字がSになるようなnを探して採用した．
4. 3から「key1の {iをkey1の長さで割った余り}番目の文字をord()で数値に戻したものに0x20を引いたもの」を引く．
5. 4に0x20を足す．
6. 5をchr()して数値からASCIIに変換する．

これで元のtextに戻るはず．
実装してみる．

```python
def decrypt(key,text):
    flag=''
    for n in range(1,10000):
        if chr(((ord(text[0])-0x20)+(0x7e-0x20+1)*n)-(ord(key[0 % len(key)])-0x20)+0x20)=='S':
            for i in range(len(text)):
                flag+=chr(((ord(text[i])-0x20)+(0x7e-0x20+1)*n)-(ord(key[i % len(key)])-0x20)+0x20)
            print(flag)
    return flag

print(key1,rev3)
```
### #ここで時間を取られた
個人的な話．ここで詰まった．(飛ばしてくれていいですよ)
以上の出力結果はこうである．

```
S¤¢¢®­{²uccess_£ecryption_¸eah_¸eah_S¤¢¢®­}
```
惜しい．非常に惜しい．エンコードミスだと思って一時間以上とられた．
実際には前述のとおりnが一意でないので最初の文字だけでnを決めてはいけなかったのである．
よく見てみるとASCIIコードの数値から微妙にずれている文字が文字化けしている．

### #なので
返り値に合わせて数値を調整する．

```python
flag=decrypt(key1,rev3)

for index in range(len(flag)):
    if(ord(flag[index])>127):
        print(chr(ord(flag[index])-(0x7e-0x20+1)),end="")
    else:
        print(flag[index],end="")

print()
```
やっと出た．

```
SECCON{Success_Decryption_Yeah_Yeah_SECCON}
```

solver全文

```python
import sys
from Crypto.Cipher import AES
import base64

def encrypt(key, text):
    s = ''
    for i in range(len(text)):
        s += chr((((ord(text[i]) - 0x20) + (ord(key[i % len(key)]) - 0x20)) % (0x7e - 0x20 + 1)) + 0x20)
    return s

def decrypt(key,text):
    flag=''
    for n in range(1,10000):
        if chr(((ord(text[0])-0x20)+(0x7e-0x20+1)*n)-(ord(key[0 % len(key)])-0x20)+0x20)=='S':
            for i in range(len(text)):
                flag+=chr(((ord(text[i])-0x20)+(0x7e-0x20+1)*n)-(ord(key[i % len(key)])-0x20)+0x20)
    return flag

key1 = "SECCON"
key2 = "seccon2019"

out="FyRyZNBO2MG6ncd3hEkC/yeYKUseI/CxYoZiIeV2fe/Jmtwx+WbWmU1gtMX9m905"

cipher = AES.new(key2 + chr(0x00) * (16 - (len(key2) % 16)), AES.MODE_ECB)

rev1=base64.b64decode(out.encode('ascii'))

rev2=cipher.decrypt(rev1)

rev3=rev2.decode('ascii').replace("\x05","")

flag=decrypt(key1,rev3)

for index in range(len(flag)):
    if(ord(flag[index])>127):
        print(chr(ord(flag[index])-(0x7e-0x20+1)),end="")
    else:
        print(flag[index],end="")

print()
```


### Thank you for playing!
サービス問題って前から二個だったっけ...?

```
SECCON{We have done all the challenges. Thank you!}
```


## おわりに
久しぶりにQiitaに記事書いた．
Writeup書く気になるまでまぁまぁ時間がかかったが問題がまだ残っていてよかった．
難読shellscriptは解けそうだったので復習しておきたい．
実質一人で解いたがもう何問か解けそうだったので残念．（やっぱりWeb系が苦手）
来週の高専のCTFに向けて復習していきたい．

