# working-container on Amazon linux

## docker-compose.yml
  - HTTP base dir is /var/www/html
  - Mount local ./base dir to container /var/www/html
  - Mount local ./data dir to container /data
  - HTTP Port is 8000
  - requeire AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY env for awscli 

## use TTY
- build and up
```
docker-compose build
docker-compose up -d
```
- enter TTY
```
docker-compose exec tanu /bin/bash
```

