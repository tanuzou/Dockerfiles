FROM amazonlinux:2017.12
LABEL Name=tanu Version=0.0.1

WORKDIR /tmp

# timezone
RUN cp -f -p /usr/share/zoneinfo/Japan /etc/localtime

# packages
RUN yum -y update && yum -y upgrade
RUN amazon-linux-extras install php7.2 ruby2.4 python3 vim
RUN yum -y install httpd httpd-tools gcc gcc-c++ make git diffutils file wget which vim re2c tar
RUN yum -y install php php-devel 
RUN yum -y install php-pdo php-fpm php-json php-mysqlnd php-pod php-common php-cli php-mbstring php-gd php-pear php-opcache 
RUN yum -y install ruby ruby-devel ruby-doc rubygem-bundler libxslt-devel libpcap-devel
RUN yum -y install python3 python3-pip python3-devel python3-tools
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

# re2c
WORKDIR /tmp
RUN git clone https://github.com/skvadrik/re2c.git re2c 
WORKDIR /tmp/re2c/re2c/
RUN ./autogen.sh && \
	./configure && \
	make && \
	make install
# Phalcon
WORKDIR /tmp
RUN git clone git://github.com/phalcon/cphalcon.git && cd cphalcon/build && ./install
RUN echo 'extension=phalcon.so' > /etc/php.d/phalcon.ini

# Phalcon-tools
WORKDIR /usr/local/share
RUN git clone git://github.com/phalcon/phalcon-devtools.git && cd phalcon-devtools && ./phalcon.sh
RUN ln -s /usr/local/share/phalcon-devtools/phalcon.php /usr/bin/phalcon

# Googld Cloud SDK, kubectl
WORKDIR /tmp
RUN wget -q https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-193.0.0-linux-x86_64.tar.gz && \
	tar zxvf google-cloud-sdk-193.0.0-linux-x86_64.tar.gz && \
	mv google-cloud-sdk /usr/local/share/
ENV PATH $PATH:/usr/local/share/google-cloud-sdk/bin
RUN /usr/local/share/google-cloud-sdk/bin/gcloud config set disable_usage_reporting true
RUN /usr/local/share/google-cloud-sdk/bin/gcloud components install kubectl

# kube-aws
WORKDIR /tmp
RUN wget -q https://github.com/kubernetes-incubator/kube-aws/releases/download/v0.9.9/kube-aws-linux-amd64.tar.gz && \
	tar zxvf kube-aws-linux-amd64.tar.gz && \
	mv linux-amd64/kube-aws /usr/local/bin

# kops
WORKDIR /tmp
RUN curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64 && \
	chmod +x kops-linux-amd64 && \
    mv kops-linux-amd64 /usr/local/bin/kops

# AWSCLI
WORKDIR /tmp
RUN wget -q https://bootstrap.pypa.io/get-pip.py && python get-pip.py
RUN pip install awscli

# Google API
## python
RUN pip install --upgrade google-api-python-client

# Apache
RUN sed -i -e "s/Listen 80/Listen 8000/" /etc/httpd/conf/httpd.conf
RUN sed -i -e "s/AllowOverride None/AllowOverride All/" /etc/httpd/conf/httpd.conf
RUN sed -i -e "s/Options Indexes FollowSymLinks/Options -Indexes +FollowSymLinks/" /etc/httpd/conf/httpd.conf

# httpd foreground
ENTRYPOINT /usr/sbin/httpd -D FOREGROUND
EXPOSE 8000

# codenize-tools
RUN gem install miam roadworker cfdef

WORKDIR /data
