# docker-laravel ð³

ã­ã¼ã«ã«ç°å¢æ§ç¯æé 

```bash
# ãªã¢ã¼ããªãã¸ããªããã¯ã­ã¼ã³
$ git clone https://github.com/kaitonishimura624/docker-laravel.git
$ cd docker-laravel
$ composer create-project "laravel/laravel=6.*" backend --prefer-dist #backendã¨ãããã­ã¸ã§ã¯ãã®ä½æ


# å¿è¦ãªã³ã³ãããèµ·å
$ docker-compose up -d 
$ docker-compose exec app bash

# Laravelè¨­å®
$ composer install
$ composer update
$ php artisan key:generate
$ chmod 777 -R storage
$ chmod 777 bootstrap/cache

# ãã¤ã°ã¬ã¼ã·ã§ã³
$ php artisan migrate --seed --env=dev

```

ãã¤ã°ã¬ã¼ã·ã§ã³ã³ãã³ã

```bash
# ãã¤ã°ã¬ã¼ã·ã§ã³å®è¡
$ php artisan migrate
$ php artisan migrate --seed

# å¨ã¦ã®ãã¼ãã«ãåé¤ãã¦ãã¤ã°ã¬ã¼ã·ã§ã³
$ php artisan migrate:fresh
$ php artisan migrate:refresh --seed

# ãã¤ã°ã¬ã¼ã·ã§ã³ç¶æ³ã®ã¹ãã¼ã¿ã¹ç¢ºèª
$ php artisan migrate:status

# ã­ã¼ã«ããã¯
$ php artisan migrate:rollback

# ãã¤ã°ã¬ã¼ã·ã§ã³çæ (æ°è¦ãã¼ãã«ã®ä½æ)
$ php artisan make:migration create_users_table --create=users

# ãã¤ã°ã¬ã¼ã·ã§ã³çæ (æ¢å­ãã¼ãã«ã®æ´æ°)
$ php artisan make:migration add_votes_to_users_table --table=users

# ã·ã¼ãã¼ã®ä½æ
$ php artisan make:seeder UsersTableSeeder

# ã·ã¼ãã¼ã®è¨­å®å®äºå¾ã«åæ 
$ composer dump-autoload

# ã¢ãã«ã®ä½æ
$ php artisan make:model Models/User

```

Dockerã³ãã³ã

```bash
# appã®ã³ã³ããã«ã¢ã¯ã»ã¹
$ docker-compose exec app bash

# ã³ã³ãããå¨ã¦åæ­¢
$ docker-compose down

# Docker volumeãå¨ã¦åé¤
$ docker volume prune

# Docker imageãå¨ã¦åé¤
$ docker image prune -a
```

mysqlåç§

```bash
# appã®ã³ã³ããã«ã¢ã¯ã»ã¹
$ docker-compose exec db bash

# mysqlã«ã­ã°ã¤ã³
$ mysql -u root -p 
password : secret

# ãã¼ã¿ãã¼ã¹ãé¸ã¶
$ use use laravel_local;

# ãã¼ãã«ãé¸ã¶
$ show users;

```

ã©ã¤ãã©ãª

```bash
# Laravel-permission
https://spatie.be/docs/laravel-permission/v3/introduction

```

## Container structure

```bash
âââ app
âââ web
âââ db
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
