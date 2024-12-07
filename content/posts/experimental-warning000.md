---
title: ExperimentalWarning が出る
date: 2024-12-07 13:21:11.236381800+0900
---

`create-next-app` を更新しろという風な表示が出たので、更新してみた。

    $ npm i -g create-next-app
    (node:9628) ExperimentalWarning: CommonJS module C:\ProgramData\Scoop\persist\nodejs\bin\node_modules\npm\node_modules\debug\src\node.js is loading ES Module C:\ProgramData\Scoop\persist\nodejs\bin\node_modules\npm\node_modules\supports-color\index.js using require().
    Support for loading ES Module in require() is an experimental feature and might change at any time
    (Use `node --trace-warnings ...` to show where the warning was created)

    added 1 package in 7s

メッセージっぽいところの翻訳はこちら:

    en:
    Support for loading ES Module in require() is an experimental feature and might change at any time
    (Use `node --trace-warnings ...` to show where the warning was created)
    
    ja:
    require() での ES モジュールのロードのサポートは実験的な機能であり、いつでも変更される可能性があります
    (警告が作成された場所を表示するには、`node --trace-warnings ...` を使用します)

`supports-color/index.js` が `debug/src/node.js` を `require` しているみたいだ。
また、`debug/src/node.js` は ES モジュールであり、これの `require` でのロードは実験的なサポートだよということを伝える warning らしい。

おそらくあまり問題はなさそうだ。

