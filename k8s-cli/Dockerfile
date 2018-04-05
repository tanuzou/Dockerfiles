FROM amazonlinux:2017.12
LABEL Name=tanu Version=0.0.1

# timezone
RUN cp -f -p /usr/share/zoneinfo/Japan /etc/localtime

# packages
RUN yum -y update && yum -y upgrade
RUN amazon-linux-extras install php7.2 ruby2.4 python3 vim
RUN yum -y install httpd httpd-tools gcc gcc-c++ make git diffutils file wget which vim re2c tar
RUN yum -y install ruby ruby-devel ruby-doc libxslt-devel
RUN yum -y install python3 python3-pip python3-devel python3-tools

# pip
WORKDIR /tmp
RUN wget -q https://bootstrap.pypa.io/get-pip.py && python get-pip.py

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

WORKDIR /data