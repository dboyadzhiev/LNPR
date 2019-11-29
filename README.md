# Install

## Docker setup

Set the system details

|variable| default value| meaning|
|---|---|---|
|PROJECT_NAME|lnp_app| project name|
|POSTGRES_PORT|5444| postgres port|
|WEBSERVER_PORT|8080| webserver port|
|REDIS_PORT|6379| redis port|
|POSTGRES_USER|postgres| postgres user name|
|POSTGRES_PASSWORD|postgres| postgres user password|
|POSTGRES_DB|postgres| postgres database name|
|PHP_VERSION|7.1| php version (it is a php fpm docker image version "php:$PHP_VERSION-fpm" )  |

If you want to set PHP ini configurations
```bash
vim docker/php-fpm/php-ini-overrides.ini
``` 

Run docker composer

```bash
docker-compose up -d
```

## Setup laravel the project

Copy the laravel project into the `application` directory 

Copy `docker/php-fpm/laravel.env` to `application/.env` and update the values if you want:
```bash
cp docker/php-fpm/laravel.env application/.env
```

- Composer install

```bash
docker-compose exec php-fpm composer install
```

- Prepare the project
```bash
docker-compose exec php-fpm php artisan key:generate 
docker-compose exec php-fpm php artisan cache:clear
docker-compose exec php-fpm php artisan config:clear
```