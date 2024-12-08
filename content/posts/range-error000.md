---
title: gatsby develop するとエラる
date: 2024-12-08 08:29:31.462703100+0900
---

エラる…。

    Error: RangeError [ERR_BUFFER_OUT_OF_BOUNDS]: "length" is outside of buffer bounds

> 「長さ」はバッファ境界外です

ってどういうことなんだ…？

そして以下がおそらくスタックトレース:

    - buffer:1066 Buffer.utf8Write
    node:internal/buffer:1066:13

    - node.cjs:1151 Packr.encodeUtf8
    [siofrey-hill]/[msgpackr]/dist/node.cjs:1151:18

