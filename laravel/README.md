# Docker laravel on Amazon linux

## docker-compose.yml
  - HTTP base dir is /var/laravel/www
  - Mount local ./base dir to container /var/laravel/www 
  - HTTP Port is 8001

## Create laravel project
- build and up
```
docker-compose build
docker-compose up -d
```
- create project
```
docker-compose exec laravel /bin/bash
cd /var/laravel/www
rm -rf *
cd /var/laravel
composer create-project --prefer-dist laravel/laravel www
```
- Website
```
http://localhost:8001/
```
