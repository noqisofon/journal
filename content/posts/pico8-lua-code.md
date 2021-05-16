---
title: "PICO-8 の Lua コード"
date: 2021-05-17T08:33:30+09:00
draft: false
---

ピクセル(水色かな？)を方向キーによって動かすコード。

``` lua
function _init()
   x = 64
   y = 64
end

function _update()
   if ( btn( LEFT  ) ) x -= 1
   if ( btn( RIGHT ) ) x += 1

   if ( btn( UP    ) ) y -= 1
   if ( btn( DOWN  ) ) y += 1
end

function _draw()
   cls()
   pset( x, y, 12 )
end
```

わぁお！ ちょー簡単だ。

スプライトの場合は `SPR` 関数を使う。

``` lua
function _draw()
   cls()
   -- 表示したいスプライトを 1 番とする。
   spr( 1, x, y )
end
```
