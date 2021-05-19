---
title: "定数の初期化の話"
date: 2020-09-30T00:00:00+09:00
draft: false
---

この辺こんな風に(キーワードは違うにせよ)書ける言語もあるんだけど、JS はダメなのよね。

``` javascript
const x;
if (cond) {
    // 一回だけ代入可
    x = hoge;
} else {
    x = fuga;
}
// x が初期化されていないパスがある状態でここで x を使うとエラー
```

たしかに。  
上記しかなかったら、こういう風に書くよね:

``` javascript
const x = cond ? hoge : fuga;
```

Scheme だとこういう風に書ける:

``` scheme
(define-constant x (if *cond*
                       hoge
                     fuga))
```

あんまり変わらないけど...。

# えーと

よく見ると、定数の初期化の話ではない......？

つまり、`const` は変数への 1
回だけの代入を許すみたいなものがある言語もあるけれども、JavaScript
では最初に代入しないと Syntax Error になってしまう。 みたいなことか。

こういうエラーが出た:

    $ deno run ./demo000.js
    error: Uncaught SyntaxError: Missing initializer in const declaration
    const x;
        ^
        at <anonymous> (file:///D:/home/rihine/workspace/2020-09-30/demo000.js:1:7)
