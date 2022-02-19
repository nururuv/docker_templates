# docker_templates

MySQL コンテナを作成する Docker テンプレート

## USAGE

1. ./services/mysql 配下に「db」フォルダを作成する
2. コンテナ作成

```
docker-compose up -d
```

コンテナの中に入る

```
docker exec -it mysql bash
```
