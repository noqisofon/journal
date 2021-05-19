---
title: "cl-charms がいんすとろーるできない"
date: 2020-10-02T00:00:00+09:00
draft: false
section: lisp
---

なぜかと言うと、以下のように `ncurses.h` をインクルードしようとしているから。

    ~\.roswell\lisp\quicklisp\dists\quicklisp\software\cl-charms-20200218-git\src\low-level\curses-grovel__grovel.c:6:10: fatal error: ncurses.h: No such file or directory
        6 | #include <ncurses.h>
    |          ^~~~~~~~~~~
    compilation terminated.

それで `MINGW64` における `ncurses` であるところの `mingw-w64-x86_64-ncurses` の `ncurses.h` が以下のように:

    $ pacman -Ql mingw-w64-x86_64-ncurses | grep 'ncurses.h'
    mingw-w64-x86_64-ncurses /mingw64/include/ncurses/ncurses.h
    mingw-w64-x86_64-ncurses /mingw64/include/ncursesw/ncurses.h

少なくとも `ncurses/ncurses.h` に置かれているので、

    $ pkg-config --cflags ncursesw
    -D_XOPEN_SOURCE=600 -D_POSIX_C_SOURCE=199506L -ID:/msys2/mingw64/include/ncursesw

`pkg-config` からもわかるように

``` c
#include <ncursesw/ncurses.h>
```

ってやらなくちゃいけないっていうか、 `pkg-config` つこおてるんだったら

``` c
#include <ncurses.h>
```

こうでも良いんじゃないかって思うんだけれどもやってないんだろうか......。