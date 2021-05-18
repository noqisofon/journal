---
title: "Perl からログを出力する方法"
date: 2021-02-11T00:00:00+09:00
draft: true
---

Perl のすくりぷよから最も簡単にログを吐くには、組み込み関数の warn を使うよ！

``` perl
warn 'request timeout';
```

これを実行すると、標準出力に対して:

    $ perl ./how_to_output_log000.pl
    request timeout at ./how_to_output_log000.pl line 5.

のように `warn` を記したファイル名と行が合わせて出力されるよ！