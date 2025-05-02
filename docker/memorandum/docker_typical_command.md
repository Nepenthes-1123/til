# dockerの代表的なコマンド

## dockerfileからimageを作る

```bash
docker build  -t $IMAGENAME (:$TAGNAME) $DOCKERFILEPATH
```

## イメージからコンテナを作る

```bash
docker container run $IMAGENAME (: $TAG)
```

- `--rm`
  - コンテナ終了時に自動削除
- `--name $CONTAINERNAME`
  - コンテナに名前をつける
- `--mount type={volume|bind|tmpfs},src=$VOLUMENAME,dst=$INPATH`
  - コンテナにボリュームをマウントする
- `-it`
  - インタラクティブモード

```bash
docker container run --rm --name atcoder_solution --mount type=volume,src=atcoder_volume,dst=/root -it atcoder:1.0
```
