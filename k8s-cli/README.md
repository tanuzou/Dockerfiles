# k8s-cli on Amazon linux

## docker-compose.yml
  - Mount local ./data dir to container /data
  - requeire AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY env for awscli 

## use TTY
- build and up
```
docker-compose build
```
- enter TTY
```
docker-compose run k8s-cli /bin/bash
```

