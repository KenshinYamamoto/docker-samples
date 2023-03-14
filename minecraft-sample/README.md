# 概要

minecraft(javaEdition)でサーバ建てて友達と一緒に遊びたかったので、dockerで実装してみた。

## 簡単な説明

初めはitzg/minecraft-serverのimageをpullし、コマンドプロンプトで

```sh
docker run -d -it --cpus 4 --memory 10g -p 25565:25565 -e EULA=TRUE --name server-test itzg/minecraft-server
```

を入力してコンテナを作成していたのだが、とにかくコマンドが長いうえに管理しづらかったので、docker-compose.ymlを作成して入力するコマンドの量を減らし、管理しやすくした。

```sh
docker-compose up -d
```

でコンテナを作成可能となった。

## コンテナ起動後

minecraft(javaEdition)を起動後、マルチプレイ→ダイレクト接続でホストPCのIPアドレスを入力することでサーバへ入室可能であることを確認した。

## minecraftの設定をいじる

コンテナを起動後、コマンドプロンプトにて

```sh
docker-compose exec minecraft-server bash
```

を入力し、/data直下のファイルなどをいじることでminecraftの設定を変更可能

## 課題

私自身のセキュリティに関する知識が乏しい為、セキュリティ的な問題の有無が不明である。
現在はホストPCの一時IPv6アドレスを使用して入室してもらっているが、安全なのかがわからない。
