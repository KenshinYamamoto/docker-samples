# 概要

dockerを使用してJupyterLabでの開発環境を作成するデモ

## ビルドコマンド

- macの場合

```sh
docker build --platform linux/amd64 .
```

- windowsの場合

```sh
docker build .
```

でイメージを作成。

## イメージ作成後

```sh
docker run -p 8888:8888 -v <マウント元ファイル>:<マウント先ファイル> --name <コンテナ名> <image>
```

でポート8888を使用してJupyterLabを起動可能。
ブラウザから**localhost:8888**に接続して使用可能。
