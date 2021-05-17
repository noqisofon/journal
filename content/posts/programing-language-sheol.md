---
title: "プログラミング言語 Sheol"
date: 2021-05-01T00:00:00+09:00
draft: false
---

Limbo をインスパイアしたプログラミング言語 Sheol のへろーわーるど:

``` text
include "sys.shl" as Sys;
include "draw.shl";

module Hello {
    init(self : ref Draw.Context, argv : list[string]);
}

init(self : ref Draw.Context, argv : list[string]) {
    sys = load Sys;

    sys->print( "Hello, World!\n" );
}
```

ここで Sys モジュールをロード:

``` text
sys = load Sys;
```

変数 `sys` は `Sys` 型。  
`Sys` は `Module` 型から派生している。  
`Sys` には `open` 、 `read` 、 `write` 、 `print` などのシステム関数が含まれている。

じゃあこれはなんなのかっていうと:

``` text
include "sys.shl" as Sys;
```

`sys.shl` をインクルードしている。 

`sys.shl` は多分こういう感じの内容で:

``` text
module Sys {
    print(format_or_value : string, ...);
}
```

シグネチャしかないため、 `load` する必要があると思われる。多分......。

それだったら、以下のようにしても良いんじゃないかって思うけど......。

``` text
Sys = load 'sys.shlm';
```
