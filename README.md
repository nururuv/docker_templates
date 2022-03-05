# README

RubyOnRails And MySQL Container templates

- Ruby version
  2.7.1
- Rails version
  6.0.4
- MySQL version
  8.0

## USAGE

### 1.Rails アプリ新規作成

```
docker-compose run web rails new . --force --no-deps --database=mysql --skip-test --webpacker
```

### 2.DB 新規作成

/services/web/config/database.yml を以下の通り修正する
※Rails アプリ新規作成済みでないと当ファイルは存在しない

```
# MySQL. Versions 5.5.8 and up are supported.
#
# Install the MySQL driver
#   gem install mysql2
#
# Ensure the MySQL gem is defined in your Gemfile
#   gem 'mysql2'
#
# And be sure to use new-style password hashing:
#   https://dev.mysql.com/doc/refman/5.7/en/password-hashing.html
#
default: &default
  adapter: mysql2
  encoding: utf8mb4
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password: Mysql@9999
  # コンテナ名
  host: mysql

# DB作成：myapp_development
development:
  <<: *default
  database: myapp_development

# DB作成：myapp_test
test:
  <<: *default
  database: myapp_test

# DB作成：myapp_production
production:
  <<: *default
  database: myapp_production
  username: myapp
  password: <%= ENV['MYAPP_DATABASE_PASSWORD'] %>

```

```
（mysql コンテナが起動している状態で）
docker-compose run web rake db:create
```

### 3.アプリケーション起動

```
docker-compose up
```
