# rails-tutorial-for-docker

## 初期化コマンド

```sh
# Dockerを立ち上げ rails new を実行する
docker compose run --rm web rails new . --force --no-deps --database=mysql
# 実行後 Dockerをビルド
docker compose build
```

上記を実行後 database.yml を修正する

```yml
default: &default
  adapter: mysql2
  encoding: utf8mb4
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password: <%= ENV.fetch("DATABASE_PASSWORD") %> #修正
  host: db #修正
  port: 3306 #修正
```

```sh
# Dockerを立ち上げる
docker compose up -d
# 実行後にDBを作成する
docker compose exec web rake db:create
```
