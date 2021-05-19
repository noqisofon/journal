---
title: "Docker Descktop for Windows をインストールしてみた"
date: 2020-10-17T00:00:00+09:00
draft: false
---

<https://hub.docker.com/editions/community/docker-ce-desktop-windows>
からインストーラーをダウンロード。

WSL2 をバックエンドとして Docker Descktop for Windows を実行していると、WSL のディストリビューション一覧は以下のようになるらしい:

``` text
PS C:\Users\alice> wsl -l -v
  NAME                   STATE           VERSION
* Debian                 Running         2
  docker-desktop         Running         2
  docker-desktop-data    Running         2
```

実際にコンテナが動作することを検証するために、今回は Amazon Linux 2 のイメージを Docker Hub から pull って実行するっぽい。

<https://hub.docker.com/_/amazonlinux>

`docker pull` でイメージを引っこ抜いてきて、 `docker run` でイメージを実行する感じなんだろうか...。

``` text
PS C:\Users\alice> docker pull amazonlinux
Using default tag: latest
latest: Pulling from library/amazonlinux
37373184fe69: Pull complete
Digest: sha256:2c99363fc74d3a39f02365b964e73cceb2b2524c00e9977e16680156e2f79ee8
Status: Downloaded newer image for amazonlinux:latest
docker.io/library/amazonlinux:latest

PS C:\Users\alice> docker run -it amazonlinux
bash-4.2# cat /etc/image-id
image_name="amzn2-container-raw"
image_version="2"
image_arch="x86_64"
image_file="amzn2-container-raw-2.0.20200722.0-x86_64"
image_stamp="3280-5fdd"
image_date="20200724160117"
recipe_name="amzn2 container"
recipe_id="17c5a58e-d7e0-fa2e-e80a-ccb0-2623-a6a5-fa48d402"
```

`run -it <イメージ名>` とすると、その場で `<イメージ名>`
が実行できるらしい。

Docker コンテナの実行状態？は `ps` サブコマンドで確認できるらしい:

``` text
PS C:\Users\alice> docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                          PORTS               NAMES
c31352b5b45b        amazonlinux         "/bin/bash"         4 minutes ago       Exited (0) About a minute ago                       awesome_lederberg
```

終了したから Exited ってなってるけど、動作してることが確認できたっぽい。