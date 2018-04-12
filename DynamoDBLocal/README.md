# DynamoDB Local on Amazon linux

## docker-compose.yml
  - Mount local ./data dir to container /data
  - DynamoDB HTTP Port is 8080
  - require AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY env for awscli 

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
- test DynamoDB Local
```
aws dynamodb list-tables --endpoint-url http://localhost:8080
```


