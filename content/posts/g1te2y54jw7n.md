---
title: Scoop をインストールしてみる
description: ぷにゃにゃー！
pubDate: 2024-12-08T22:44:51.889832+09:00
draft: false
---

## インストールする

PowerShell を起動し、以下のように打つ:

``` powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

インストールできたら、とりあえずバージョンを表示してみる:

``` powershell
scoop --version
```

表示できたら多分インストールできたことが確認できたと思われる。

## インストールしたあと

`pandoc` をインストールしてみると良いんじゃないかなぁ。

``` powershell
scoop install pandoc
```

## バケット

`scoop` は `bucket` を追加してインストールできるアプリを増やしていけるので、デフォルトで入ってるやつ以外のを使いたいという場合は `bucket` を追加してみよう。

`extra` を追加するには以下のように打つよ:

``` powershell
scoop add bucket extras
```
