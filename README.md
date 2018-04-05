# Dockerfile based on AmazonLinux

This repository is Dockerfile based on AmazonLinux image for any work.

# aws-cli
- BaseImage
  - Amazon Linux
- Include
  - ruby, python, AWSCLI



# k8s-cli
- BaseImage
  - Amazon Linux 2 (2817.12)
- Include
  - ruby24, python AWSCLI, Google Cloud SDK, kubectl, kube-aws, kops

# laravel
- BaseImage
  - Amazon Linux
- Include
  - httpd24, php71, Composer



# phalcon
- BaseImage: Amazon Linux
- Include: httpd24, php71, Composer, Phalcon



# working-container (all include)
- BaseImage: Amazon Linux 2 (2817.12)
- Include: httpd24, php72, ruby24, python3, AWSCLI, Google Cloud SDK, kubectl, kube-aws, kops, phalcon



