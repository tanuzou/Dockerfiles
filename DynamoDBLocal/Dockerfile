FROM amazonlinux:2017.12
LABEL Name=dynamodb Version=0.0.1

WORKDIR /tmp

# timezone
RUN cp -f -p /usr/share/zoneinfo/Japan /etc/localtime

# packages
RUN yum -y update && yum -y upgrade
RUN amazon-linux-extras install php7.2 ruby2.4 python3 vim
RUN yum -y install make git diffutils file wget which vim tar
RUN yum -y install java-1.8.0-openjdk java-1.8.0-openjdk-headless java-1.8.0-openjdk-devel

# pip
WORKDIR /tmp
RUN wget -q https://bootstrap.pypa.io/get-pip.py && python get-pip.py

# PHP
RUN echo 'date.timezone = Asia/Tokyo' >> /etc/php.ini

# PHP Composer
WORKDIR /tmp
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# AWSCLI
WORKDIR /tmp
RUN wget -q https://bootstrap.pypa.io/get-pip.py && python get-pip.py
RUN pip install awscli

# DynamoDB Local
ENV JAVA_HOME /usr/lib/jvm/java
RUN mkdir /usr/local/share/dynamodb
RUN cd /usr/local/share/dynamodb && \
    wget -q https://s3-ap-northeast-1.amazonaws.com/dynamodb-local-tokyo/dynamodb_local_latest.tar.gz && \
    tar zxvf dynamodb_local_latest.tar.gz

# start
CMD ["java", "-Djava.library.path=/usr/local/share/dynamodb/DynamoDBLocal_lib", "-jar", "/usr/local/share/dynamodb/DynamoDBLocal.jar", "-dbPath", "/data"]
EXPOSE 8000

WORKDIR /data
