---
title: Cloudflare Pages に deploy できない
description: ぷにゃにゃー！
date: 2024-12-07T16:18:34.977694+09:00
draft: false
---

Cloudflare の Pages にデプロイしてみたときのこと。
ビルド時のログである:

    2024-12-07T03:50:14.068214Z	Executing user command: npx next build
    2024-12-07T03:50:14.925762Z	You are using Node.js 18.17.1. For Next.js, Node.js version >= v18.18.0 is required.
    2024-12-07T03:50:14.940442Z	Failed: Error while executing user command. Exited with error code: 1
    2024-12-07T03:50:14.948947Z	Failed: build command exited with code: 1
    2024-12-07T03:50:15.639809Z	Failed: error occurred while running build command

さて、ローカルにおける `node` のバージョンは以下の通りである:

    $ node --version
    v23.3.0

つまり、Cloudflare Pages における `node` のバージョンは `v18.17.1` なのだが、`npx next build` を実行するのに必要なバージョンは `v18.18.0` 以上なのである。
これではコマンドを実行できず、デプロイが失敗する…。

Next.js 以外のフレームワークを使った方が良いようである…。
