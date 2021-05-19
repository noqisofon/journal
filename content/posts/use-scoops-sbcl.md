---
title: "Scoop の SBCL を使用する"
date: 2021-05-20T08:45:04+09:00
draft: false
---

Scoop で SBCL をインストールしても、sbcl
はコアファイルが変なところにあると思っていて探しても見つからないので、
実行できない。

変なところっていうか、インストーラーが既定のパスにしているところなので、変ではないんだけども……。

とりあえず、新しくコアファイルを `$HOME/.sbcl` に作成することにする。

既定のところに Scoop
をインストールしていれば、以下のようなスクリプトでコアファイルを作成できるはず:

``` shell-script
[ ! -d $HOME/.sbcl ] && mkdir -p $HOME/.sbcl 

sbcl --core /c/ProgramData/Scoop/apps/sbcl/current/sbcl.core --noinform --no-print --no-userinit <<EOF
; loading asdf and asdf-install library
;(require :asdf)
;(require :asdf-install)

; dumping image
(save-lisp-and-die
 (merge-pathnames ".sbcl/sbcl.core" (user-homedir-pathname))
 :purify t)
EOF
```

これでコアファイルはできたので、以下のようなハローワールド系コードを実行してみよう:

``` commonlisp
(write-line "Hello, World!")
```

だが、sbcl は `C:/Program Files/sbcl/` に入っているコアファイルを見てしまう。

    $ sbcl --script ./hello.lisp
    fatal error encountered in SBCL pid 20796(tid 00000000001D68F0):
    can't find core file at C:Program Files/sbcl/lib/sbcl//sbcl.core

なので、 `--core` オプションを指定して先ほど作成したコアファイルを見るようにしてみるとうまくいく。

    $ sbcl --core $HOME/.sbcl/sbcl.core --script ./hello.lisp
    Hello, World!

読み込むコアファイルを設定ファイルで指定できれば良いのだが……。

## `SBCL_HOME` の指定

調べてみると、 `SBCL_HOME` という環境変数を指定すれば良いようだ。

上記の例で言えば、以下のようにすれば、 `--core` オプションの指定が不必要になる:

``` shell-script
export SBCL_HOME=$HOME/.sbcl
```

    $ sbcl --script ./hello.lisp
    Hello, World!

# 参考

- https://www.math.s.chiba-u.ac.jp/~matsu/cl/sbcl.html