---
title: abs の動きを書いてみる
description: ぷにゃにゃー！
pubDate: 2024-12-10T20:27:33.937034+09:00
draft: false
---

以下の `abs` というワードを定義したとする。

``` forth
: abs ( n -- |n| )
  dup 0< 
  if
    negate
  then
;
```

以下のように -7 を渡してみたときのことを考える。

``` forth
-7 abs
```

`-7` というワードは、-7 という数値をスタックに積む。

Forth はスタック思考言語であり、スタックでものを考える。
スタックが共にあらんことを。

先ほど定義した `abs` というワードはスタックの一番上にある数値を絶対値に変更する。

`abs` の中身に移っていくわけだが、最初のワードは `dup` でこれはスタックの一番上の値をもっかい積む。
先ほど -7 が積まれたので、スタックの中身はもっかい -7 が積まれて多分こうなっているはず:

```
  +--------+
  |   -7   |
  +--------+
  |   -7   |
--+--------+---
```

次の `0<` というワードはいわゆる `0 <` という 2 つのワードのショートカットだ。
Lisp でも `1+` というものがあって、Forth でもあるがこれはスタックの一番上に 1 を足すというものだ。
で、`0<` というワードの動きに移るが、これは `-7 0 <` という風に並べられたものに等しい。

Lisp で書けばこうだ:

``` lisp
(< -7 0)  ;; => t
```

-7 と 0 とでは 0 の方が大きいため、`negate` というワードが来る。
`negate` が評価？される前のスタックの中身はこうだ:

```
  +--------+
  |   -7   |
--+--------+---
```

`negate` というワードはスタックの一番上の値の符号を反転する。
ここでスタックの一番上は -7 なので、-7 の符号が反転し、7 になる。
そういうわけで、スタックの中身はこうなる:

```
  +--------+
  |    7   |
--+--------+---
```

ということで、評価が終わった。
