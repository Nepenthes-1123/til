# git commandをまとめる

はじめてのメモということで代表的なgitのコマンドについてまとめてみる

## コミットの一連の流れ

```bash
git add $FILENAME
git commit -m "$MESSAGE"
```

## ローカルリポジトリをリモートにプッシュ

```bash
git init
git branch -M main
git add .
git commit -m "$MASAGE"
git remote add origint $URL
git push -u origin main
```

## リモート関連

### リモートからクローンする

ローカルでの名称を変更したい場合、ファイル名を指定

```bash
git clone $URL ($FILENAME)
```

### リモートから変更を取得

どちらでもよい

```bash
git pull
```

```bash
git fetch
git merge origin/main
```

### リモートにプッシュ

```bash
git push origin $BRANCHNAME
```

たいてい[`git remote`](#リモートと紐づける)を使ってリモートを登録しているため以下のコマンドで大丈夫

```bash
git push
```

### リモートと紐づける

```bash
git remote add origin $URL
```

## config設定

### gitの初期設定で使う

```bash
git config --global user.name "$USER.NAME"
git config --global user.email "$USER.EMAIL"
```

### gitの設定を確認

```bash
git config --global --list
```
