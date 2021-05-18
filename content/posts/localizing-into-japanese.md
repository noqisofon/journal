---
title: "Ubuntu の日本語化"
date: 2020-10-25T23:56:59+09:00
draft: false
---

``` {.text}
% sudo vim /etc/locale.gen
```

vim とかで編集して、 `ja_JP.utf8` をコメントインする。

``` {.text}
% sudo locale-gen
```

を実行して有効にする。

``` {.text}
% localectl set-locale LANGUAGE=ja_JP.utf8
```

`localectl` を使って `ja_JP.utf8` を選択する。
あとは再起動すれば日本語化されている。

