---
title: KOSENセキュリティコンテスト2019 Writeup
date: 2019-11-05T00:00:00+09:00
description: KOSENセキュリティコンテスト2019のWriteup
hideToc: false
enableToc: true
enableTocContent: false
author: Takana Norimasa
tags:
- CTF
categories:
- event
draft: false
---

> この記事は[KOSENセキュリティコンテスト2019 Writeup - Qiita](https://qiita.com/Seigenkousya/items/46078afbec2ddfc09d3f)から移転してきたものです．

## はじめに
10/26に開催されたKOSENセキュリティコンテスト2019に出場してきた．今年で3回目．
今年は例年と違って1日のみの6時間と大幅短い時間での開催になった．
結果は1160点で16位．もう少し頑張れた気もするけど，まぁこれが今の実力かなぁとも思った．
もっと精進せねば...

## Writeup
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/2bdd282c-7503-efdb-887e-e0c11ba3bb7f.png)
問題が即削除されたのでかなり曖昧です...
運営さんはあれだけWriteupを書くことを推奨していたんだから問題を残しておいて（切実
とりあえず，.zsh_historyと記憶を頼りに解いた順に書いてく．

## 09 プログラミング言語を当てよう
早速，詰まった．いろいろ試したがヒットしないし，その割りに解答率がいいので話題のアレかとなった．（確か，returnを使った特徴的な記法で気がついた気がする．）

```
function inc(num)
  num = num + 1
  return num

class ClassName(name)
  @name = name
  @function output()
    print("Hello, ")
    print(self.name)
    return
```
この言語の名前はBlawnなので問題文の通り（確かそう），大文字で

```
CTFKIT{BLAWN}
```
## 17 目に見えなくても
問題に書いてあるリンクを踏むと何もかかれていないページが．
ページのソースを見るとflagが書いてある．
![Screenshot from 2019-11-04 23-26-56.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/a51e9c92-f64b-e608-8099-0ba35b60cb94.png)

```
CTFKIT{html_may_be_including_hidden_text}
```

## 12 大人たちの無意味な慣習
pcap問題．
とりあえずhtmlとcssとzipがあったのでエクスポート．
![Screenshot from 2019-11-04 21-53-48.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/9a4e8b83-2601-6a1d-763c-c1ba13e812c4.png)
適当にhtmlを眺めてみると，
![Screenshot from 2019-11-04 21-55-51.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/bd345ac2-5fff-5ef9-68f6-d715ca300ddb.png)
なんてこったい．
さっきエクスポートしたzipファイルにこのパスワードを突っ込んで解凍すると，

```
CTFKIT{majide_muimina_shuukan_dayonee}
```

##06 無言のELF
バイナリ問題．
実行すると無言で文字列の受付けをする．手がかりはなし．
gdb-pedaに投げる．


<details><summary>アセンブラ全文</summary><div>

```
gdb-peda$ pdisass 
Dump of assembler code for function main:
   0x000055555555480a <+0>:	push   rbp
   0x000055555555480b <+1>:	mov    rbp,rsp
   0x000055555555480e <+4>:	push   r15
   0x0000555555554810 <+6>:	push   r14
   0x0000555555554812 <+8>:	push   r13
   0x0000555555554814 <+10>:	push   r12
   0x0000555555554816 <+12>:	push   rbx
   0x0000555555554817 <+13>:	sub    rsp,0x168
   0x000055555555481e <+20>:	mov    rax,QWORD PTR fs:0x28
   0x0000555555554827 <+29>:	mov    QWORD PTR [rbp-0x38],rax
   0x000055555555482b <+33>:	xor    eax,eax
   0x000055555555482d <+35>:	movabs rax,0x676665646362615f
   0x0000555555554837 <+45>:	movabs rdx,0x6f6e6d6c6b6a6968
   0x0000555555554841 <+55>:	mov    QWORD PTR [rbp-0x170],rax
   0x0000555555554848 <+62>:	mov    QWORD PTR [rbp-0x168],rdx
   0x000055555555484f <+69>:	movabs rax,0x7776757473727170
   0x0000555555554859 <+79>:	movabs rdx,0x34333231307a7978
   0x0000555555554863 <+89>:	mov    QWORD PTR [rbp-0x160],rax
   0x000055555555486a <+96>:	mov    QWORD PTR [rbp-0x158],rdx
   0x0000555555554871 <+103>:	mov    DWORD PTR [rbp-0x150],0x38373635
   0x000055555555487b <+113>:	mov    WORD PTR [rbp-0x14c],0x39
   0x0000555555554884 <+122>:	mov    rdx,QWORD PTR [rip+0x200785]        # 0x555555755010 <stdin@@GLIBC_2.2.5>
   0x000055555555488b <+129>:	lea    rax,[rbp-0x140]
   0x0000555555554892 <+136>:	mov    esi,0x100
   0x0000555555554897 <+141>:	mov    rdi,rax
   0x000055555555489a <+144>:	call   0x5555555546c0 <fgets@plt>
   0x000055555555489f <+149>:	lea    rax,[rbp-0x140]
   0x00005555555548a6 <+156>:	lea    rsi,[rip+0x22b]        # 0x555555554ad8
   0x00005555555548ad <+163>:	mov    rdi,rax
   0x00005555555548b0 <+166>:	call   0x5555555546e0 <strtok@plt>
   0x00005555555548b5 <+171>:	lea    rax,[rbp-0x140]
   0x00005555555548bc <+178>:	lea    rsi,[rip+0x217]        # 0x555555554ada
   0x00005555555548c3 <+185>:	mov    rdi,rax
   0x00005555555548c6 <+188>:	call   0x5555555546d0 <strcmp@plt>
   0x00005555555548cb <+193>:	test   eax,eax
   0x00005555555548cd <+195>:	jne    0x555555554a0e <main+516>
   0x00005555555548d3 <+201>:	movzx  eax,BYTE PTR [rbp-0x161]
   0x00005555555548da <+208>:	movsx  esi,al
   0x00005555555548dd <+211>:	movzx  eax,BYTE PTR [rbp-0x150]
   0x00005555555548e4 <+218>:	movsx  edi,al
   0x00005555555548e7 <+221>:	movzx  eax,BYTE PTR [rbp-0x15c]
   0x00005555555548ee <+228>:	movsx  r8d,al
   0x00005555555548f2 <+232>:	movzx  eax,BYTE PTR [rbp-0x16b]
   0x00005555555548f9 <+239>:	movsx  r9d,al
   0x00005555555548fd <+243>:	movzx  eax,BYTE PTR [rbp-0x168]
   0x0000555555554904 <+250>:	movsx  eax,al
   0x0000555555554907 <+253>:	mov    DWORD PTR [rbp-0x174],eax
   0x000055555555490d <+259>:	movzx  eax,BYTE PTR [rbp-0x160]
   0x0000555555554914 <+266>:	movsx  ebx,al
   0x0000555555554917 <+269>:	mov    DWORD PTR [rbp-0x178],ebx
   0x000055555555491d <+275>:	movzx  eax,BYTE PTR [rbp-0x152]
   0x0000555555554924 <+282>:	movsx  ecx,al
   0x0000555555554927 <+285>:	mov    DWORD PTR [rbp-0x17c],ecx
   0x000055555555492d <+291>:	movzx  eax,BYTE PTR [rbp-0x15c]
   0x0000555555554934 <+298>:	movsx  edx,al
   0x0000555555554937 <+301>:	mov    DWORD PTR [rbp-0x180],edx
   0x000055555555493d <+307>:	movzx  eax,BYTE PTR [rbp-0x16b]
   0x0000555555554944 <+314>:	movsx  r15d,al
   0x0000555555554948 <+318>:	movzx  eax,BYTE PTR [rbp-0x170]
   0x000055555555494f <+325>:	movsx  r14d,al
   0x0000555555554953 <+329>:	movzx  eax,BYTE PTR [rbp-0x15e]
   0x000055555555495a <+336>:	movsx  r13d,al
   0x000055555555495e <+340>:	movzx  eax,BYTE PTR [rbp-0x16e]
   0x0000555555554965 <+347>:	movsx  r12d,al
   0x0000555555554969 <+351>:	movzx  eax,BYTE PTR [rbp-0x168]
   0x0000555555554970 <+358>:	movsx  ebx,al
   0x0000555555554973 <+361>:	movzx  eax,BYTE PTR [rbp-0x160]
   0x000055555555497a <+368>:	movsx  r11d,al
   0x000055555555497e <+372>:	movzx  eax,BYTE PTR [rbp-0x167]
   0x0000555555554985 <+379>:	movsx  r10d,al
   0x0000555555554989 <+383>:	mov    DWORD PTR [rbp-0x184],r10d
   0x0000555555554990 <+390>:	movzx  eax,BYTE PTR [rbp-0x150]
   0x0000555555554997 <+397>:	movsx  r10d,al
   0x000055555555499b <+401>:	movzx  eax,BYTE PTR [rbp-0x16e]
   0x00005555555549a2 <+408>:	movsx  ecx,al
   0x00005555555549a5 <+411>:	movzx  eax,BYTE PTR [rbp-0x160]
   0x00005555555549ac <+418>:	movsx  edx,al
   0x00005555555549af <+421>:	movzx  eax,BYTE PTR [rbp-0x168]
   0x00005555555549b6 <+428>:	movsx  eax,al
   0x00005555555549b9 <+431>:	push   rsi
   0x00005555555549ba <+432>:	push   rdi
   0x00005555555549bb <+433>:	push   r8
   0x00005555555549bd <+435>:	push   r9
   0x00005555555549bf <+437>:	mov    esi,DWORD PTR [rbp-0x174]
   0x00005555555549c5 <+443>:	push   rsi
   0x00005555555549c6 <+444>:	mov    edi,DWORD PTR [rbp-0x178]
   0x00005555555549cc <+450>:	push   rdi
   0x00005555555549cd <+451>:	mov    esi,DWORD PTR [rbp-0x17c]
   0x00005555555549d3 <+457>:	push   rsi
   0x00005555555549d4 <+458>:	mov    edi,DWORD PTR [rbp-0x180]
   0x00005555555549da <+464>:	push   rdi
   0x00005555555549db <+465>:	push   r15
   0x00005555555549dd <+467>:	push   r14
   0x00005555555549df <+469>:	push   r13
   0x00005555555549e1 <+471>:	push   r12
   0x00005555555549e3 <+473>:	push   rbx
   0x00005555555549e4 <+474>:	push   r11
   0x00005555555549e6 <+476>:	mov    r9d,DWORD PTR [rbp-0x184]
   0x00005555555549ed <+483>:	mov    r8d,r10d
   0x00005555555549f0 <+486>:	mov    esi,eax
   0x00005555555549f2 <+488>:	lea    rdi,[rip+0xff]        # 0x555555554af8
   0x00005555555549f9 <+495>:	mov    eax,0x0
   0x00005555555549fe <+500>:	call   0x5555555546b0 <printf@plt>
=> 0x0000555555554a03 <+505>:	add    rsp,0x70
   0x0000555555554a07 <+509>:	mov    eax,0x0
   0x0000555555554a0c <+514>:	jmp    0x555555554a1f <main+533>
   0x0000555555554a0e <+516>:	lea    rdi,[rip+0x113]        # 0x555555554b28
   0x0000555555554a15 <+523>:	call   0x555555554690 <puts@plt>
   0x0000555555554a1a <+528>:	mov    eax,0x1
   0x0000555555554a1f <+533>:	mov    rbx,QWORD PTR [rbp-0x38]
   0x0000555555554a23 <+537>:	xor    rbx,QWORD PTR fs:0x28
   0x0000555555554a2c <+546>:	je     0x555555554a33 <main+553>
   0x0000555555554a2e <+548>:	call   0x5555555546a0 <__stack_chk_fail@plt>
   0x0000555555554a33 <+553>:	lea    rsp,[rbp-0x28]
   0x0000555555554a37 <+557>:	pop    rbx
   0x0000555555554a38 <+558>:	pop    r12
   0x0000555555554a3a <+560>:	pop    r13
   0x0000555555554a3c <+562>:	pop    r14
   0x0000555555554a3e <+564>:	pop    r15
   0x0000555555554a40 <+566>:	pop    rbp
   0x0000555555554a41 <+567>:	ret    
End of assembler dump.
```

</div></details>
とりあえず動かして流れを読む．

```
gdb-peda$ start
```

適当にnextを押していたら終わってしまった．
しかし，途中でstrcompとjneの分岐があった．非常に怪しい．
ここをうまく分岐の中に入れればいい感じなんじゃないか？
そこでjne命令のところでflag（レジスタの方）を書き換える．

```
gdb-peda$ info registers eflags
eflags         0x282               [ SF IF ]

gdb-peda$ set $eflags ^= (1 << 6)
gdb-peda$ info registers eflags
eflags         0x2c2               [ ZF SF IF ]
```
ゼロフラグを書き換えた．これでジャンプしないはず．
ジャンプしないまま続けるとレジスタにそれっぽい文字列が出てき始める．

![Screenshot from 2019-11-04 22-16-18.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/55662ecd-4cf8-fef9-14b3-3e6ee46fe02c.png)

しばらくまたnextで進めていくとprintfにぶつかりflagが出力される．

```
CTFKIT{hpb5iphbr_et3phet5o}
```
gdbだと出力がすぐに次に行っちゃって分かり辛いので注意．

## 02 伝統的な暗号
確かキーの長さが三文字と問題文に書いてあった．
換字式暗号であることは間違いないが，3文字って何...?
結構時間がかかった問題．
与えられた文字列：UAPCPD{vv_e_cuyo_csylxwyo_upzzlb?}

とりあえず，CTFKITの文字は確定してるのでCとU，TとA，FとP...と六文字の文字の距離を測ってみる．

```python
def dist(y,x):
    counter=0

    x=ord(x.lower())
    y=ord(y.lower())

    while(True):
        if(x==y):
            return counter

        y+=1
        #print(chr(y))
        counter+=1
        if(y==ord('z')+1):
            y=ord('a')

given="UAPCPD{vv_e_cuyo_csylxwyo_upzzlb?}"
flag_format="CTFKIT"

for i in range(len(flag_format)):
    print(dist(given[i],flag_format[i]),end=" ")

print()
```
すると，

```
8 19 16 8 19 16
```
周期的な並びが出てくる．
つまり，8個ずらす，19個ずらす，16個ずらす...を繰り替えしているっぽい．
これを与えられた文字列すべてにやれば大丈夫そう．
ただし，記号は例外なので除外しておく．

```python
def shift(x,y):
    x=x.lower()
    ret=ord(x)+y

    if(ret>ord('z')):
        ret=ord('a')+(ret-ord('z')-1)

    return chr(ret)

def decrypt(given):
    counter=0
    for i in (range(len(given))):
        if(ord(given[i])>ord('a') and (given[i] != '{' and given[i] != '}' and given[i] != '_' )):
            if(counter%3==0):
                print(shift(given[i],8),end="")
            elif(counter%3==1):
                print(shift(given[i],19),end="")
            elif(counter%3==2):
                print(shift(given[i],16),end="")
            counter+=1
        else:
            print(given[i],end="")


given="UAPCPD{vv_e_cuyo_csylxwyo_upzzlb?}"
flag_format="CTFKIT"

print(flag_format,end="")
decrypt(given[6:])
print()
```

```
CTFKIT{do_u_know_vigenere_cipher?}
```
どうやら[ヴィジュネル暗号](https://ja.wikipedia.org/wiki/%E3%83%B4%E3%82%A3%E3%82%B8%E3%83%A5%E3%83%8D%E3%83%AB%E6%9A%97%E5%8F%B7)というらしい．

## 14 お茶をさぐれ
友達から急に解き途中のプログラムが渡されて訳も分からず解いた．
一応途中からだけど書き残す．

といっても多分もう終盤．apkのファイルまで抽出できているのでこれを好きな言語で書き直して実行するだけ．

<details><summary>もらったapk</summary><div>

```java
live:yuhma5 ，12:37
package com.example.ureshino.ctfmondai_android;

import android.animation.Animator;
import android.animation.AnimatorListenerAdapter;
import android.annotation.TargetApi;
import android.app.LoaderManager;
import android.content.CursorLoader;
import android.content.Loader;
import android.database.Cursor;
import android.net.Uri;
import android.os.AsyncTask;
import android.os.Build;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.support.annotation.NonNull;
import android.support.design.widget.Snackbar;
import android.support.v7.app.AppCompatActivity;
import android.text.TextUtils;
import android.view.KeyEvent;
import android.view.View;
import android.view.ViewPropertyAnimator;
import android.widget.ArrayAdapter;
import android.widget.AutoCompleteTextView;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import java.util.ArrayList;
import java.util.List;

public class LoginActivity extends AppCompatActivity implements LoaderManager.LoaderCallbacks<Cursor> {
  private static final String[] DUMMY_CREDENTIALS = { "herfuvab@sr2b3.wc:tenaoyhr" };
  
  private static final int REQUEST_READ_CONTACTS = 0;
  
  private UserLoginTask mAuthTask = null;
  
  private AutoCompleteTextView mEmailView;
  
  private View mLoginFormView;
  
  private EditText mPasswordView;
  
  private View mProgressView;
  
  private boolean LoginTask(String paramString1, String paramString2) {
    String[] arrayOfString = DUMMY_CREDENTIALS;
    int i = arrayOfString.length;
    boolean bool = false;
    for (byte b = 0; b < i; b++) {
      String[] arrayOfString1 = nyaho(arrayOfString[b]).split(":");
      if (arrayOfString1[0].equals(paramString1))
        bool = arrayOfString1[1].equals(paramString2); 
    } 
    return bool;
  }
  
  private void addEmailsToAutoComplete(List<String> paramList) {
    ArrayAdapter arrayAdapter = new ArrayAdapter(this, 17367050, paramList);
    this.mEmailView.setAdapter(arrayAdapter);
  }
  
  private void attemptLogin() {
    if (this.mAuthTask != null)
      return; 
    this.mEmailView.setError(null);
    this.mPasswordView.setError(null);
    String str1 = this.mEmailView.getText().toString();
    String str2 = this.mPasswordView.getText().toString();
    byte b2 = 0;
    StringBuilder stringBuilder = null;
    byte b1 = b2;
    AutoCompleteTextView autoCompleteTextView = stringBuilder;
    if (!TextUtils.isEmpty(str2)) {
      b1 = b2;
      autoCompleteTextView = stringBuilder;
      if (!isPasswordValid(str2)) {
        this.mPasswordView.setError(getString(2131558449));
        autoCompleteTextView = this.mPasswordView;
        b1 = 1;
      } 
    } 
    if (TextUtils.isEmpty(str1)) {
      this.mEmailView.setError(getString(2131558446));
      AutoCompleteTextView autoCompleteTextView1 = this.mEmailView;
      b1 = 1;
    } else if (!isEmailValid(str1)) {
      this.mEmailView.setError(getString(2131558448));
      autoCompleteTextView = this.mEmailView;
      b1 = 1;
    } 
    if (b1 != 0) {
      autoCompleteTextView.requestFocus();
      return;
    } 
    if (LoginTask(str1, str2)) {
      TextView textView = (TextView)findViewById(2131230792);
      textView.setVisibility(0);
      stringBuilder = new StringBuilder();
      stringBuilder.append(f());
      stringBuilder.append(l());
      stringBuilder.append(o());
      stringBuilder.append(g());
      stringBuilder.append(g2());
      stringBuilder.append(e());
      stringBuilder.append(h());
      stringBuilder.append(i());
      stringBuilder.append(j());
      stringBuilder.append(k());
      stringBuilder.append(l2());
      stringBuilder.append(n());
      stringBuilder.append(o2());
      String str = stringBuilder.toString();
      StringBuilder stringBuilder1 = new StringBuilder();
      stringBuilder1.append("CTFKIT{");
      stringBuilder1.append(nyaho(str));
      stringBuilder1.append("}");
      textView.setText(stringBuilder1.toString());
      return;
    } 
    this.mEmailView.setError("Login Failed.... ((((((((((っ･ω･)っ ");
    ((TextView)findViewById(2131230792)).setVisibility(4);
    this.mEmailView.requestFocus();
  }
  
  private boolean isEmailValid(String paramString) { return paramString.contains("@"); }
  
  private boolean isPasswordValid(String paramString) { return (paramString.length() > 4); }
  
  private boolean mayRequestContacts() {
    if (Build.VERSION.SDK_INT < 23)
      return true; 
    if (checkSelfPermission("android.permission.READ_CONTACTS") == 0)
      return true; 
    if (shouldShowRequestPermissionRationale("android.permission.READ_CONTACTS")) {
      Snackbar.make(this.mEmailView, 2131558459, -2).setAction(17039370, new View.OnClickListener() {
            @TargetApi(23)
            public void onClick(View param1View) { LoginActivity.this.requestPermissions(new String[] { "android.permission.READ_CONTACTS" }, 0); }
          });
      return false;
    } 
    requestPermissions(new String[] { "android.permission.READ_CONTACTS" }, 0);
    return false;
  }
  
  private void populateAutoComplete() {
    if (!mayRequestContacts())
      return; 
    getLoaderManager().initLoader(0, null, this);
  }
  
  @TargetApi(13)
  private void showProgress(final boolean show) {
    int i = Build.VERSION.SDK_INT;
    int k = 0;
    int j = 0;
    if (i >= 13) {
      float f1;
      k = getResources().getInteger(17694720);
      View view2 = this.mLoginFormView;
      if (paramBoolean) {
        i = 8;
      } else {
        i = 0;
      } 
      view2.setVisibility(i);
      ViewPropertyAnimator viewPropertyAnimator2 = this.mLoginFormView.animate().setDuration(k);
      float f2 = 1.0F;
      if (paramBoolean) {
        f1 = 0.0F;
      } else {
        f1 = 1.0F;
      } 
      viewPropertyAnimator2.alpha(f1).setListener(new AnimatorListenerAdapter() {
            public void onAnimationEnd(Animator param1Animator) {
              byte b;
              View view = LoginActivity.this.mLoginFormView;
              if (show) {
                b = 8;
              } else {
                b = 0;
              } 
              view.setVisibility(b);
            }
          });
      View view1 = this.mProgressView;
      if (paramBoolean) {
        i = j;
      } else {
        i = 8;
      } 
      view1.setVisibility(i);
      ViewPropertyAnimator viewPropertyAnimator1 = this.mProgressView.animate().setDuration(k);
      if (paramBoolean) {
        f1 = f2;
      } else {
        f1 = 0.0F;
      } 
      viewPropertyAnimator1.alpha(f1).setListener(new AnimatorListenerAdapter() {
            public void onAnimationEnd(Animator param1Animator) {
              byte b;
              View view = LoginActivity.this.mProgressView;
              if (show) {
                b = 0;
              } else {
                b = 8;
              } 
              view.setVisibility(b);
            }
          });
      return;
    } 
    View view = this.mProgressView;
    if (paramBoolean) {
      i = 0;
    } else {
      i = 8;
    } 
    view.setVisibility(i);
    view = this.mLoginFormView;
    i = k;
    if (paramBoolean)
      i = 8; 
    view.setVisibility(i);
  }
  
  public String e() { return "v"; }
  
  public String f() { return "h"; }
  
  public String g() { return "f"; }
  
  public String g2() { return "u"; }
  
  public String h() { return "a"; }
  
  public String i() { return "b"; }
  
  public String j() { return "_"; }
  
  public String k() { return "g"; }
  
  public String l() { return "e"; }
  
  public String l2() { return "r"; }
  
  public String n() { return "n"; }
  
  public String nyaho(String paramString) {
    char[] arrayOfChar = new char[paramString.length()];
    byte b;
    for (b = 0; b < paramString.length(); b++) {
      char c;
      char c1 = paramString.charAt(b);
      if (c1 >= 'a' && c1 <= 'm') {
        c = (char)(c1 + '\r');
      } else if (c1 >= 'A' && c1 <= 'M') {
        c = (char)(c1 + '\r');
      } else if (c1 >= 'n' && c1 <= 'z') {
        c = (char)(c1 - '\r');
      } else {
        c = c1;
        if (c1 >= 'N') {
          c = c1;
          if (c1 <= 'Z')
            c = (char)(c1 - '\r'); 
        } 
      } 
      arrayOfChar[b] = c;
    } 
    return String.valueOf(arrayOfChar);
  }
  
  public String o() { return "r"; }
  
  public String o2() { return "_"; }
  
  protected void onCreate(Bundle paramBundle) {
    super.onCreate(paramBundle);
    setContentView(2131427356);
    this.mEmailView = (AutoCompleteTextView)findViewById(2131230778);
    populateAutoComplete();
    this.mPasswordView = (EditText)findViewById(2131230832);
    this.mPasswordView.setOnEditorActionListener(new TextView.OnEditorActionListener() {
          public boolean onEditorAction(TextView param1TextView, int param1Int, KeyEvent param1KeyEvent) {
            if (param1Int == 6 || param1Int == 0) {
              LoginActivity.this.attemptLogin();
              return true;
            } 
            return false;
          }
        });
    ((Button)findViewById(2131230780)).setOnClickListener(new View.OnClickListener() {
          public void onClick(View param1View) { LoginActivity.this.attemptLogin(); }
        });
    this.mLoginFormView = findViewById(2131230812);
    this.mProgressView = findViewById(2131230813);
  }
  
  public Loader<Cursor> onCreateLoader(int paramInt, Bundle paramBundle) { return new CursorLoader(this, Uri.withAppendedPath(ContactsContract.Profile.CONTENT_URI, "data"), ProfileQuery.PROJECTION, "mimetype = ?", new String[] { "vnd.android.cursor.item/email_v2" }, "is_primary DESC"); }
  
  public void onLoadFinished(Loader<Cursor> paramLoader, Cursor paramCursor) {
    ArrayList arrayList = new ArrayList();
    paramCursor.moveToFirst();
    while (!paramCursor.isAfterLast()) {
      arrayList.add(paramCursor.getString(0));
      paramCursor.moveToNext();
    } 
    addEmailsToAutoComplete(arrayList);
  }
  
  public void onLoaderReset(Loader<Cursor> paramLoader) {}
  
  public void onRequestPermissionsResult(int paramInt, @NonNull String[] paramArrayOfString, @NonNull int[] paramArrayOfInt) {
    if (paramInt == 0 && paramArrayOfInt.length == 1 && paramArrayOfInt[0] == 0)
      populateAutoComplete(); 
  }
  
  private static interface ProfileQuery {
    public static final int ADDRESS = 0;
    
    public static final int IS_PRIMARY = 1;
    
    public static final String[] PROJECTION = { "data1", "is_primary" };
  }
  
  public class UserLoginTask extends AsyncTask<Void, Void, Boolean> {
    private final String mEmail;
    
    private final String mPassword;
    
    UserLoginTask(String param1String1, String param1String2) {
      this.mEmail = param1String1;
      this.mPassword = param1String2;
    }
    
    protected Boolean doInBackground(Void... param1VarArgs) {
      try {
        Thread.sleep(100L);
        String[] arrayOfString = DUMMY_CREDENTIALS;
        int i = arrayOfString.length;
        for (byte b = 0; b < i; b++) {
          String[] arrayOfString1 = arrayOfString[b].split(":");
          if (arrayOfString1[0].equals(this.mEmail))
            arrayOfString1[1].equals(this.mPassword); 
        } 
        return Boolean.valueOf(true);
      } catch (InterruptedException param1VarArgs) {
        return Boolean.valueOf(false);
      } 
    }
    
    protected void onCancelled() {
      LoginActivity.access$402(LoginActivity.this, null);
      LoginActivity.this.showProgress(false);
    }
    
    protected void onPostExecute(Boolean param1Boolean) {
      LoginActivity.access$402(LoginActivity.this, null);
      LoginActivity.this.showProgress(false);
      if (param1Boolean.booleanValue()) {
        LoginActivity.this.finish();
        return;
      } 
      LoginActivity.this.mPasswordView.setError(LoginActivity.this.getString(2131558447));
      LoginActivity.this.mPasswordView.requestFocus();
    }
  }
}
```

</div></details>

どう考えてもここが怪しい．

```java
      stringBuilder = new StringBuilder();
      stringBuilder.append(f());
      stringBuilder.append(l());
      stringBuilder.append(o());
      stringBuilder.append(g());
      stringBuilder.append(g2());
      stringBuilder.append(e());
      stringBuilder.append(h());
      stringBuilder.append(i());
      stringBuilder.append(j());
      stringBuilder.append(k());
      stringBuilder.append(l2());
      stringBuilder.append(n());
      stringBuilder.append(o2());
      String str = stringBuilder.toString();
      StringBuilder stringBuilder1 = new StringBuilder();
      stringBuilder1.append("CTFKIT{");
      stringBuilder1.append(nyaho(str));
      stringBuilder1.append("}");

```
適当な関数から文字列をもらってそれを結合，それをさらにnyahoという関数にかけてflag化してる．

```java
  public String e() { return "v"; }
  public String f() { return "h"; }
  public String g() { return "f"; }
  public String g2() { return "u"; }
  public String h() { return "a"; }
  public String i() { return "b"; }
  public String j() { return "_"; }
  public String k() { return "g"; }
  public String l() { return "e"; }
  public String l2() { return "r"; }
  public String n() { return "n"; }
  
  public String nyaho(String paramString) {
    char[] arrayOfChar = new char[paramString.length()];
    byte b;
    for (b = 0; b < paramString.length(); b++) {
      char c;
      char c1 = paramString.charAt(b);
      if (c1 >= 'a' && c1 <= 'm') {
        c = (char)(c1 + '\r');
      } else if (c1 >= 'A' && c1 <= 'M') {
        c = (char)(c1 + '\r');
      } else if (c1 >= 'n' && c1 <= 'z') {
        c = (char)(c1 - '\r');
      } else {
        c = c1;
        if (c1 >= 'N') {
          c = c1;
          if (c1 <= 'Z')
            c = (char)(c1 - '\r'); 
        } 
      } 
      arrayOfChar[b] = c;
    } 
    return String.valueOf(arrayOfChar);
  }
```
必要な情報はすべてもらったソースコードにあるのでpythonに書き換えて復号していく．
まず，nyahoに与えられる文字列strだが，これは気合で集めた．（は？
あとはnyahoを以下のスクリプトに書き直せば完成．

```python
def decrypt(given):
    counter=0
    for i in (range(len(given))):
        c=ord(given[i])
        if(c >= ord('a') and c <= ord('m')):
            print(chr(c+ord('\r')),end="")
        elif(c >= ord('A') and c <= ord('M')):
            print(chr(c+ord('\r')),end="")
        elif(c >= ord('n') and c <= ord('z')):
            print(chr(c-ord('\r')),end="")
        else:
            if(c>=ord('N')):
                if(c<=ord('Z')):
                    print(chr(c-ord('\r')),end="")
                else:
                    print(chr(c),end="")
            else:
                print(chr(c),end="")

given="herfuvab_grn_"

print("CTFKIT{",end="")
decrypt(given)
print("}")
```

```
CTFKIT{ureshino_tea_}
```

## 13 名前を解決したい
DNSの問題．もうサーバは動いてないので記憶と記録頼り．
DNSの設定ミスで名前解決ができなくて与えられたリンクにアクセスできない．
与えられたURL:http://futuregadget-9.tech

とりあえず，digをうって確認．

```
$ dig http://futuregadget-9.tech

; <<>> DiG 9.11.5-P4-1-Debian <<>> http://futuregadget-9.tech
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 61541
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;http://futuregadget-9.tech.	IN	A

;; AUTHORITY SECTION:
tech.			3600	IN	SOA	ns0.centralnic.net. hostmaster.centralnic.net. 262197 900 1800 6048000 3600

;; Query time: 99 msec
;; SERVER: 192.168.0.1#53(192.168.0.1)
;; WHEN: 月 11月 04 23:06:27 JST 2019
;; MSG SIZE  rcvd: 120
```
有力な情報は見つからない．
あれこれオプションを試してみるが芳しくない．
（後で他の人のwriteupを見たらこれでいけていた．何で？（殺意））

自分の場合は以下でうまくいった．

```
dig http://futuregadget-9.tech -p80
```
textにIPがあることは分かっていたのになぁ...
なんでダメだったんだろう．

IPが出てくるのでそこにアクセスする．

![Screenshot from 2019-11-04 23-28-58.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/a441e92a-34fb-4932-b94b-076987497367.png)

```
CTFKIT{naki_nureshi_megami_no_kikan}
```


## 20 偉くなりたい
自分が閃いて解いたのだが，肝心のhtmlが無いので解説できない．
見つかり次第追記するが，htmlのhidden属性のフォームが隠されていてそのフォームの属性をtextに変えてその欄にデフォルトでかかれている```is_not_admin```を```is_admin```に変えて送信するとflagが落ちてくる仕組み．
自分でもよく閃いたと思う．

## 10 ツートントン
割とよくあるモールス問題．
以下のような画像が与えられる．
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/458b205d-570a-3863-d4e5-c3490f821e47.png)
小さいので拡大するとこう．（これがまずかった．）
![2morlse.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/bb876a8f-05ba-ea17-78b0-92d10313d073.png)
どうやらこれがモールスの並びっぽい．
画像のピクセルを読んでビットに置き換える．
ところが，さっき拡大してしまったのでどこのピクセルの値を取るかで迷ってしまった．
ここでかなり時間を取られた．実は，親切にも最初の画像が1ドット1ピクセルになってた．（友達に言われるまで気づかなかった）
とりあえず，ビットに起こす．

```python
import cv2

img=cv2.imread("image.png")
h,w,c=img.shape

x=45
y=45

print(h,w)

for i in range(x):
    for j in range(y):
        if(img[i,j][0]):
            print("+",end="")
        else:
            print("-",end="")

    print()
```

```
45 45
+-----++++++--++--++--++--++++++--++--++++++-
-++--++--++++++++++++++--++--++++++--++--++--
++++++++++++++-----++-----++++++-----++-----+
+-----++++++--++-----++--++++++--++--++--++++
++--++++++++++++++-----++--++-----++--++++++-
----++-----++-----++++++-----++--++--++++++--
++++++--++-----++--++-----++--++-----++++++++
++++++-----++--++-----++--++++++--++-----++++
++-----++--++++++++++++++-----++--++-----++--
---++++++-----++-----++-----++++++--++--++---
--++++++++++++++--++--++-----++--++++++--++--
++++++-----++--++++++-----++--++--+++++++++++
+++-----++++++--++--++--++--++++++--+++++++++
+++++--++--++-----++--++++++--++-----++--++--
++++++--++-----++++++-----++-----++--++++++--
++--++-----++-----++--++--++++++++++++++-----
++++++--++--++--++--++++++--++++++++++++++--+
+--++-----++--++++++--++-----++--++--++++++--
++-----++++++-----++-----++--++++++++++++++--
++--++++++--++--++--++++++++++++++-----++--++
-----++--++++++-----++++++--++--++-----++--++
++++-----++--++-----++++++--++--++++++-----++
++++-----++--++-----++-----++--++++++-----+++
+++--++--++-----++++++--++--++-----++++++----
-++--++--++--++-----++++++-----++++++-----++-
----++-----++++++-----++--++++++-----++--++--
++--++-----++++++-----++++++-----++-----++---
--++++++-----++--++++++-----++--++--++--++---
--++++++-----++++++--++--++-----++++++--++--+
+-----++++++-----++--++--++--++-----++++++---
--++++++-----++-----++-----++++++-----++--+++
+++-----++--++-----++-----++--++-----++++++++
++++++--++--++--++--++++++--++-----++++++--++
--++--++--++++++--++-----++++++-----++-----++
--++--++-----++-----++++++++++++++-----++--++
-----++--++++++--++-----++++++-----++--++++++
++++++++-----++--++-----++-----++++++-----++-
----++-----++++++--++--++-----++++++++++++++-
-++--++-----++--++++++--++--++++++-----++--++
++++-----++--++--++++++++++++++--++--++++++--
---++++++--++--++-----++-----++--++--++++++++
+++++++++++++++++++++++++++++++++++++++++++++
+++++++++++++++++++++++++++++++++++++++++++++
+++++++++++++++++++++++++++++++++++++++++++++
+++++++++++++++++++++++++++++++++++++++++++++
```

これをモールス信号に整形する．
短音がマイナス2つ，長音がマイナス5つ，単語の区切りがプラス6つなのを考慮して置換する．（よく考えたらプラスとマイナス逆だなぁ...

置換したものがこちらになります．

```
_ .... .. ...   .. ...   __ ___ ._. ... .   _._. ___ _.. . ._._._   _._. ._ _.   _.__ ___ .._   .._. .. _. _..   _ .... .   .._. ._.. ._ __. ..__..   _ .... .   .._. ._.. ._ __.   .. ...   _._. _ .._. _._ .. _ _.__. _ .._ .._ _..._ _ ___ _. _..._ _ ___ _. _..._ _ .._ .._ _..._ _ ___ _. _.__._   .... ._ .... ._ __..__   _._. ._ _.   _.__ ___ .._   .._. .. _. _..   .. _ ..__..                                                 
```
後はこれをwebのツールに投げておしまい．

![Screenshot from 2019-11-04 23-57-31.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/332794/569081ef-09d8-f1fb-ade1-6625d9797ca2.png)


括弧は問題文の通り置換する．

```
CTFKIT{TUU=TON=TON=TUU=TON}
```

# 感想
一週間も間が空いてしまったがコマンドの履歴とソルバとかファイルが残っていてぎりぎり書けた．
難しいだろうけど運営は問題をWriteup用にしばらく残して（切実
偉くなりたいは頼みのキャッシュにページが無かったので探し中．もし見つかったら追記する．
こうみると結構解いたなぁと思う．頑張った自分．
まだまだ実力と経験不足なのでこれからも精進したい．

## 追記
書いたデータが知らず知らずのうちに消えてた（全ギレ
投稿した矢先に編集してすいません．
睡眠時間を返して．

