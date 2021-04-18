# docker-laravel 🐳

ローカル環境構築手順

```bash
# リモートリポジトリからクローン
$ git clone https://github.com/kaitonishimura624/docker-laravel.git
$ cd docker-laravel
$ composer create-project "laravel/laravel=6.*" backend --prefer-dist #backendというプロジェクトの作成


# 必要なコンテナを起動
$ docker-compose up -d 
$ docker-compose exec app bash

# Laravel設定
$ composer install
$ composer update
$ php artisan key:generate
$ chmod 777 -R storage
$ chmod 777 bootstrap/cache

# マイグレーション
$ php artisan migrate --seed --env=dev

```

マイグレーションコマンド

```bash
# マイグレーション実行
$ php artisan migrate
$ php artisan migrate --seed

# 全てのテーブルを削除してマイグレーション
$ php artisan migrate:fresh
$ php artisan migrate:refresh --seed

# マイグレーション状況のステータス確認
$ php artisan migrate:status

# ロールバック
$ php artisan migrate:rollback

# マイグレーション生成 (新規テーブルの作成)
$ php artisan make:migration create_users_table --create=users

# マイグレーション生成 (既存テーブルの更新)
$ php artisan make:migration add_votes_to_users_table --table=users

# シーダーの作成
$ php artisan make:seeder UsersTableSeeder

# シーダーの設定完了後に反映
$ composer dump-autoload

# モデルの作成
$ php artisan make:model Models/User

```

Dockerコマンド

```bash
# appのコンテナにアクセス
$ docker-compose exec app bash

# コンテナを全て停止
$ docker-compose down

# Docker volumeを全て削除
$ docker volume prune

# Docker imageを全て削除
$ docker image prune -a
```

mysql参照

```bash
# appのコンテナにアクセス
$ docker-compose exec db bash

# mysqlにログイン
$ mysql -u root -p 
password : secret

# データベースを選ぶ
$ use use laravel_local;

# テーブルを選ぶ
$ show users;

```

ライブラリ

```bash
# Laravel-permission
https://spatie.be/docs/laravel-permission/v3/introduction

```

## Container structure

```bash
├── app
├── web
└── db
```

### app container

- Base image
  - [php](https://hub.docker.com/_/php):8.0-fpm-buster
  - [composer](https://hub.docker.com/_/composer):2.0

### web container

- Base image
  - [nginx](https://hub.docker.com/_/nginx):1.18-alpine
  - [node](https://hub.docker.com/_/node):14.2-alpine

### db container

- Base image
  - [mysql](https://hub.docker.com/_/mysql):8.0

#### Persistent MySQL Storage

By default, the [named volume](https://docs.docker.com/compose/compose-file/#volumes) is mounted, so MySQL data remains even if the container is destroyed.
If you want to delete MySQL data intentionally, execute the following command.

```bash
$ docker-compose down -v && docker-compose up
```
