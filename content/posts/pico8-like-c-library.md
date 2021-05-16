---
title: "PICO-8 っぽい C ライブラリ"
date: 2021-05-17T08:35:57+09:00
draft: false
---

仮にぴょこ(pyoco)と名前をつけることにする。

ぴょこはフレームワークではなくてソースコードをバッと渡されて、それをビルドするみたいな方向性で行こうと思う。
例えば `gane.c` に空の `init()` 、 `update()` 、 `draw()`
が書いてあって、それに書き足したりするというような方法で 開発していく。

とりあえず、サンプルコード？で見た関数をそのまま宣言したのを書いておく:

``` c
/*!
 * 画面をまっさらにします。
 */
PYC_API void cls(void);
```

``` c
/*!
 * 画面の (x, y) の位置に指定された色番号 color_no のピクセルを表示します。
 *
 * \param x        表示したいピクセルの x 座標位置。
 * \param y        表示したいピクセルの y 座標位置。
 * \param color_no 表示したいピクセルの色番号。
 *
 * \return 成功したら `PYC_SUCCESS`、失敗したら多分 `PYC_FAILURE`。
 */
PYC_API int32_t pset(int32_t x, int32_t y, int32_t color_no);
```

``` c
/*!
 * 指定された番号のスプライトを画面の指定された位置(x, y)に表示します。
 *
 * \param no          スプライト番号。
 * \param x           スプライトを表示する x 座標。
 * \param y           スプライトを表示する y 座標。
 *
 * \return 成功したら `PYC_SUCCESS`、失敗したら多分 `PYC_FAILURE`。
 */
PYC_API int32_t spr(int32_t no, int32_t x, int32_t y);
```
