---
title: "UIM の現在の入力方式を得る"
date: 2020-04-27T00:00:00+09:00
draft: false
---

以下のようにやればいいことが分かった:

    % uim-sh -e default-im-name
    mozc

Emacs Lisp では以下のように書く:

``` emacs-lisp
;; string-trim-right は (require 'subr-x) して使う。
(string-trim-right (shell-command-to-string "uim-sh -e default-im-name"))
```

