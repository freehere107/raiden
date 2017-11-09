FROM daocloud.io/ubuntu:14.04

MAINTAINER Sun <sunbobin@itering.com>

ADD sources.list /etc/apt/sources.list

ADD get-pip.py /opt

RUN apt-get update -y && apt-get dist-upgrade -y

## python
RUN apt-get install -y \
    python \
    vim

## pip
RUN python opt/get-pip.py

RUN apt-get update -y && \
    apt-get install -y \
    git \
    gcc \
    libffi-dev \
    python-dev \
    openssl \
    libssl-dev \
    libxml2-dev \
    libxslt1-dev \
    zlib1g-dev  \
    build-essential \
    software-properties-common \
    curl

ADD requirements.txt /home

ADD pip.conf /root/.pip/pip.conf

## python package
RUN pip install --upgrade -r /home/requirements.txt

## libstdc++
RUN add-apt-repository -y ppa:ubuntu-toolchain-r/test  && \
    apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y libstdc++6

## Parity
RUN curl https://get.parity.io -Lk

## solcapt-get update
RUN add-apt-repository -y ppa:ethereum/ethereum && \
    apt-get update -y && \
    apt-get install solc -y


## pyethapp
RUN apt-get install -y \
    automake \
    pkg-config \
    libtool \
    libgmp-dev

RUN pip install pyethapp

