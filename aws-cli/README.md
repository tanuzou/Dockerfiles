# aws-cli on Amazon linux

## docker-compose.yml
  - Mount local ./data dir to container /data
  - requeire AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY env for awscli 

## use TTY
- build
```
docker-compose build
```
- enter TTY
```
docker-compose run aws-cli /bin/bash
```

