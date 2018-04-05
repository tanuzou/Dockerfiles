FROM amazonlinux
LABEL Name=aws-cli Version=0.0.1

WORKDIR /tmp

RUN cp -f -p /usr/share/zoneinfo/Japan /etc/localtime

RUN yum -y update && yum -y upgrade
RUN yum -y install gcc make git diffutils file vim which wget

RUN yum -y install ruby24 
RUN yum -y install python36 python36-pip python36-devel python36-tools

# AWSCLI
WORKDIR /tmp
RUN wget -q https://bootstrap.pypa.io/get-pip.py && python get-pip.py
RUN pip install awscli

