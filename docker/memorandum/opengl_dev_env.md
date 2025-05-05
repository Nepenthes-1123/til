# OpenGL開発環境 in Docker in WSL2を作ってみる

どうやら一般的ではないらしいので[参考記事](#参考文献)を見ながら何をしてるかまとめる。

## 環境

- WSL2
- Docker導入済み
- NVIDIAグラフィックスドライバー未導入

## Dockerfile

[参考元](#1)で用意されていたもの

```dockerfile
FROM python:3.10-slim-buster

ARG UID
ARG GID
ARG USERNAME
ARG GROUPNAME

RUN apt update && apt upgrade -y
RUN apt install libglfw3-dev python3-pip -y

RUN mkdir -p /opt/app

COPY main.py /opt/app

RUN groupadd -g $GID $GROUPNAME
RUN useradd -m -u $UID -g $GID $USERNAME

RUN chown $USERNAME:$GROUPNAME -R /opt/app
USER $USERNAME

RUN pip install glfw PyOpenGL numpy

WORKDIR /opt/app
ENTRYPOINT ["/bin/bash"]
```

[参考元](#2)で用意されていたもの

```dockerfile
FROM ubuntu:20.04

RUN apt-get update

ARG WORK_DIR=/opt
WORKDIR ${WORK_DIR}

CMD ["/bin/bash"]
```

```ymal:docker-compose.yml
services:
  docker-for-wslg:
    build: .
    environment:
      - DISPLAY=$DISPLAY
      - WAYLAND_DISPLAY=$WAYLAND_DISPLAY
      - XDG_RUNTIME_DIR=$XDG_RUNTIME_DIR
      - PULSE_SERVER=$PULSE_SERVER
    restart: always
    tty: true
    volumes:
      - /tmp/.X11-unix:/tmp/.X11-unix
      - /mnt/wslg:/mnt/wslg
```

後者の方が自身の環境に近いのでこちらを採用する。

どうやらcomposeのversionは廃止されたようなので変更した。

今回はOpenGLの開発環境を作ることが目的だったのでcomposeファイルの中身には触れないが、いずれcomposeも扱えるように学習すること。

## テンプレートを使ってDockerコンテナを作成

```bash
docker compose up -d --build
docker compose exec docker-for-wslg /bin/bash
```

ここでの`-d`はデタッチモードのオプションらしい

- `-d`
  - バックグラウンドでコンテナを起動する

## 参考文献

### 1

[【2022年版】Docker+GLFWでOpenGLプログラミング環境構築](https://qiita.com/asuka1975/items/5384ff4c20accb87cdca)

### 2

[WSLg を使って Docker 上で GUI アプリを動かす（GPUサポート付き）](https://blog.mohyo.net/2022/02/11591/)
