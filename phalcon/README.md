# Docker phalcon on Amazon linux

## docker-compose.yml
  - HTTP base dir is /var/www/html
  - Mount local ./base dir to container /var/www/html
  - HTTP Port is 8000

## Create phalcon project
- build and up
```
docker-compose build
docker-compose up -d
```
- create project
```
docker-compose exec phalcon /bin/bash
cd /var/www/html
phalcon create-project site
```

- Website
```
http://localhost:8000/site/
```