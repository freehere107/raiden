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

# pypyethereum
WORKDIR /opt

RUN git clone https://github.com/LefterisJP/pyethereum

RUN pip uninstall -y ethereum

RUN cd pyethereum && \
    git checkout take_solidity_interface_into_account && \
    pip install -r requirements.txt && \
    python setup.py install

RUN mkdir /blockchain

WORKDIR /blockchain

#geth
RUN apt-get install -y \
    nodejs \
    npm \
    ethereum

#pm2
RUN npm --registry https://registry.npm.taobao.org install -g pm2

ADD pm2.json /blockchain/pm2.json

RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN git clone https://github.com/freehere107/raiden

RUN pip install coincurve==4.5.1

RUN cd raiden && python setup.py develop

ADD parity_1.8.2_amd64.deb /opt

RUN dpkg -i /opt/parity_1.8.2_amd64.deb && rm parity_1.8.2_amd64.deb

EXPOSE 5001