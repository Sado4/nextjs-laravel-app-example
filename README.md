# Next.js × Laravel の環境構築

## 前提

- M1Mac対応
- Intel製チップMacの場合は`.docker/db/Dockerfile`を以下の通り修正
- Windowsでの動作確認は行っていない

```diff
- FROM mysql:8.0
+ FROM --platform=linux/x86_64 mysql:8.0

ENV TZ=UTC

COPY my.cnf /etc/my.cnf
```

## 使用技術

- frontend: TypeScript/React/Next.js
- backend(api): PHP/Laravel
- infra: Docker/Docker Compose

## コンテナ起動(初回ビルド)

```sh
# 初回
docker-compose up -d --build
# ２回目以降
docker-compose up -d 
```

## Laravelインストール

```sh
docker-compose exec api composer create-project laravel/laravel .
```

`api`ディレクトリ内にLaravelがインストールされる

`localhost:80`にアクセスするとLaravelのウェルカムページが表示される

## Next.jsインストール

```sh
docker-compose exec front yarn create next-app  --typescript .

# 開発用サーバー起動
docker-compose exec front yarn dev
```

`front`ディレクトリ内にNext.jsがインストールされる

`localhost:3000`にアクセスするとNext.jsのウェルカムページが表示される

開発用サーバーの停止は`control + c`
