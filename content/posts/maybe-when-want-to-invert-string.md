---
title: "Raku で文字列を反転したい時にたぶんやること"
date: 2021-05-17T08:41:18+09:00
lastUpdated: 2021-05-18T12:20:00+09:00
draft: false
---

多分こんな風にやると思うんだけど:

``` raku
say 'begin'.reverse;                        # => (begin)
```

このコードは `'begin'`
という文字列を配列の中に突っ込んだものを返すということを行う。

というのも `.reverse` は `Mu` で定義されてはいるけれど、リスト用のメソッドなので、 `.reverse` は
`'begin'` という文字列を要素が 1 つあるリストとみなしてしまう。

となればあとは簡単で、文字列を文字ごとにバラバラにして(`.split('')`)反転し(`.reverse`)、からの結合(`.join( '' )`)を行えば
文字列を反転できるはずだ。

``` raku
say 'begin'.split('').reverse.join('');     # => nigeb
```

で、 `Str` クラスにはそのものズバリのメソッド `.flip` が存在する:

``` raku
say 'begin'.flip;                           # => nigeb
```
