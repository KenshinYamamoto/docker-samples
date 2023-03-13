# 概要

LocalPC(Mac)で作成したdocker imageをSFTPを使用してAWS(Host)へアップロードし、SSHで接続してAWS上でコンテナを作成するデモ

## Dockerfile、Docker image作成

```Dockerfile
FROM alpine

RUN touch test
```

上記の簡単なDockerfileをLocalPCで作成し、

```sh
docker build --platform linux/amd64 .
```

でDocker imageを作成した。

## Docker imageをtarで圧縮する

Docker imageは(基本的に)容量が大きいので、tarファイルへ変換する。

```sh
docker save <image> > <tarファイル名>.tar
```

## tarファイルをAWSへアップロードする

tarファイルをAWSへアップロードする為にまずSFTPを使用してAWSへ接続する。

```sh
sftp -i <key名>.pem ubuntu@<publicDNS>
```

接続が完了したら、

```sh
put <tarファイルのpath> <送り先のpath>
```

でtarファイルを任意の送り先へ送信する。(多分相対パス)

## (メモ)SFTPを使用してダウンロードする方法

```sh
get <ダウンロードするファイルのpath> <ダウンロード先のpath>
```

でAWSから任意のファイル(ディレクトリ)をダウンロード可能。(多分相対パス)

## tarファイルを解凍する

```sh
ssh -i <key名>.pem ubuntu@<publicDNS>
```

SSHでAWSへ接続後、

```sh
docker load < <tarファイル名>.tar
```

を実行することでtarファイルを解凍してDocker imageとして使用可能となる。

## Containerを作成してshellを起動

alpineにはbashが無かったのでshellを起動するようにした。

```sh
docker run -it <image> sh
```

## testのファイルの存在を確認

shellにおいてlsコマンドでtestファイルがあることを確認した。
このtestファイルはDockerfileから作成したもの。
