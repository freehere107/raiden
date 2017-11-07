FROM daocloud.io/ubuntu:14.04

MAINTAINER Sun <sunbobin@itering.com>

ADD sources.list /etc/apt/sources.list

ADD get-pip.py /opt

RUN apt-get update -y && apt-get dist-upgrade -y

RUN apt-get install -y \
    python \
    vim

RUN python opt/get-pip.py

RUN apt-get install -y \
    git \
    gcc \
    libffi-dev \
    python-dev \
    openssl \
    libssl-dev \
    libxml2-dev \
    libxslt1-dev \
    zlib1g-dev  \
    build-essential

ADD requirements.txt /home

ADD pip.conf /root/.pip/pip.conf

RUN pip install --upgrade -r /home/requirements.txt

#RUN apt-get install -y software-properties-common && \
#    add-apt-repository -y ppa:ethereum/ethereum && \
#    apt-get update -y
#    apt-get install ethereum -y
